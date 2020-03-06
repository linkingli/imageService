1.harbor做双主复制
2.harbor集群挂载分布式cephfs存储
3.在k8s集群上部署harbor

几种策略的比较
```
1.第二种和第三种都是多个节点，然后挂载的分布式存储，然后为了保证数据的统一性使用单独的mysql数据库，这样以来存在mysql数据和镜像仓库数据单点存放，故障恢复难度大，安装操作复杂的问题
2.双主复制不存在这些问题，数据多点存放，而且扩容更改高可用模式操作简单，可以更换成主主从等模式。

```

双朱复制
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

```
