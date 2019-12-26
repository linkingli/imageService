# imageService
imageService
docker pull registry.cn-hangzhou.aliyuncs.com/lilisi/lilisi:[镜像版本号]
```

vi /etc/docker/daemon.json
{
“registry-mirrors”: [“https://registry.docker-cn.com“]
}

systemctl daemon-reload
systemctl restart docker

```
