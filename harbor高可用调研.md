```
1.harbor做双主复制
2.harbor集群挂载分布式cephfs存储，
3.在k8s集群上部署harbor
```
几种策略的比较
```
1.第二种和第三种都是多个节点，然后挂载的分布式存储，然后为了保证数据的统一性使用单独的mysql数据库，这样以来存在mysql数据和镜像仓库数据单点存放，故障恢复难度大，安装操作复杂的问题
2.双主复制不存在这些问题，数据多点存放，而且扩容更改高可用模式操作简单，可以更换成主主从等模式。

```

双主复制
```

$ wget https://github.com/vmware/harbor/releases/download/v1.1.2/harbor-online-installer-v1.1.2.tgz
$ tar xvf harbor-online-installer-v1.1.2.tgz


主要配置文件:
harbor.conf   在hostname配置多节点如10.125.30.125，10.125.30.126

# cat harbor.cfg 
_version = 1.5.0
hostname = repository.skong.com
ui_url_protocol = https
max_job_workers = 50 
customize_crt = on
ssl_cert = /data/harbor-data/cert/repository.crt
ssl_cert_key = /data/harbor-data/cert/repository.key
secretkey_path = /data/harbor-data/
admiral_url = NA
log_rotate_count = 50
100k, size 100M and size 100G 
log_rotate_size = 200M
http_proxy =
https_proxy =
no_proxy = 127.0.0.1,localhost,ui
email_identity = 
email_server = smtp.mydomain.com
email_server_port = 25
email_username = sample_admin@mydomain.com
email_password = abc
email_from = admin <sample_admin@mydomain.com>
email_ssl = false
email_insecure = false
harbor_admin_password = Harbor123456
auth_mode = db_auth
ldap_url = ldaps://ldap.mydomain.com
ldap_basedn = ou=people,dc=mydomain,dc=com
ldap_uid = uid 
ldap_scope = 2 

ldap_timeout = 5
ldap_verify_cert = true
ldap_group_basedn = ou=group,dc=mydomain,dc=com
ldap_group_filter = objectclass=group
ldap_group_gid = cn
ldap_group_scope = 2
token_expiration = 30
project_creation_restriction = everyone
db_host = mysql
db_password = root123
db_port = 3306
db_user = root
redis_url = redis:6379
clair_db_host = postgres
clair_db_password = password
clair_db_port = 5432
clair_db_username = postgres
clair_db = postgres
uaa_endpoint = uaa.mydomain.org
uaa_clientid = id
uaa_clientsecret = secret
uaa_verify_cert = true
uaa_ca_cert = /path/to/ca.pem
registry_storage_provider_name = filesystem
registry_storage_provider_config =
################################################################


这种方式安装的hat仍然需要使用高可用的存储
  registry:
    image: vmware/registry-photon:v2.6.2-v1.5.0
    container_name: registry
    restart: always
    volumes:
      - /data/harbor-data/registry:/storage:z
      - ./common/config/registry/:/etc/registry/:z
    networks:
      - harbor 
    environment:
      - GODEBUG=netdns=cgo
    command:
      ["serve", "/etc/registry/config.yml"]
    depends_on:
      - log
    logging:
      driver: "syslog"
      options:  
        syslog-address: "tcp://127.0.0.1:1514"
        tag: "registry"


问题:
harbor官方默认提供主从复制的方案来解决镜像同步问题，通过复制的方式，我们可以实时将测试环境harbor仓库的镜像同步到生产环境harbor，类似于如下流程：

harbor1

在实际生产运维的中，往往需要把镜像发布到几十或上百台集群节点上。这时，单个Registry已经无法满足大量节点的下载需求，因此要配置多个Registry实例做负载均衡。手工维护多个Registry实例上的镜像，将是十分繁琐的事情。Harbor可以支持一主多从的镜像发布模式，可以解决大规模镜像发布的难题：

harbor2

只要往一台Registry上发布，镜像就像“仙女散花”般地同步到多个Registry中，高效可靠。

如果是地域分布较广的集群，还可以采用层次型发布方式，如从集团总部同步到省公司，从省公司再同步到市公司：

harbor3

然而单靠主从同步，仍然解决不了harbor主节点的单点问题。

双主复制说明
所谓的双主复制其实就是复用主从同步实现两个harbor节点之间的双向同步，来保证数据的一致性，然后在两台harbor前端顶一个负载均衡器将进来的请求分流到不同的实例中去，只要有一个实例中有了新的镜像，就是自动的同步复制到另外的的实例中去，这样实现了负载均衡，也避免了单点故障，在一定程度上实现了Harbor的高可用性：

harbor5

这个方案有一个问题就是有可能两个Harbor实例中的数据不一致。假设如果一个实例A挂掉了，这个时候有新的镜像进来，那么新的镜像就会在另外一个实例B中，后面即使恢复了挂掉的A实例，Harbor实例B也不会自动去同步镜像，这样只能手动的先关掉Harbor实例B的复制策略，然后再开启复制策略，才能让实例B数据同步，让两个实例的数据一致。

另外，我还需要多吐槽一句，在实际生产使用中，主从复制十分的不靠谱。
```
分布式存储
```
多个Harbor实例共享同一个后端存储，任何一个实例持久化到存储的镜像，都可被其他实例中读取。通过前置LB进来的请求，可以分流到不同的实例中去处理，
这样就实现了负载均衡，也避免了单点故障

风险：
1：共享存储的选取，Harbor的后端存储目前支持AWS S3、Openstack Swift, Ceph等，

2：Session在不同的实例上共享，这个现在其实已经不是问题了，在最新的harbor中，默认session会存放在redis中，我们只需要将redis独立出来即可。可以通过redis sentinel或者redis cluster等方式来保证redis的可用性。目前的5.0的harbor未配套redis.

3：Harbor多实例数据库问题，这个也只需要将harbor中的数据库拆出来独立部署即可。让多实例共用一个外部数据库，数据库的高可用也可以通过数据库的高可用方案保证。-5.0的os已经有mysql可以做到ha
```

分布式存储VSAN：http://www.dockerinfo.net/2656.html
·


