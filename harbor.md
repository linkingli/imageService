```

default                    os-harbor-admreg-5468d67469-nvb5d                     2/2       Running             0          22h       10.240.0.207    paas-m3       <none>
default                    os-harbor-jobserver-dc8f86b94-2d28h                   1/1       Running             4          6d        10.242.1.57     paas-m02      <none>
default                    os-harbor-nginx-84ff85b55b-wvk5t                      1/1       Running             0          22h       10.242.1.103    paas-m02      <none>
default                    os-harbor-ui-f9598465b-ghhgs                          1/1       Running             12         7d        10.241.0.131    paas-m1       <none>

os-harbor-admreg
image: registry/admin:v1.1.0

os-harbor-jobserver
image: harbor-jobservice:v1.1.0

os-harbor-nginx
image: nginx:v1.13.1

os-harbor-ui
image: harbor-ui:v1.1.0
```
```
https://ruzickap.github.io/k8s-harbor/#links
```

```
my-release-harbor-chartmuseum-79b8f54596-7dcb9     0/1     ContainerCreating   0          84s
my-release-harbor-clair-7899bb4c98-tw62r           0/2     ContainerCreating   0          84s
my-release-harbor-core-6cdf99c79d-wdlf7            0/1     ContainerCreating   0          84s
my-release-harbor-database-0                       0/1     Init:0/2            0          73s
my-release-harbor-jobservice-5576977f59-k6ftr      0/1     ContainerCreating   0          84s
my-release-harbor-notary-server-7cb669b47f-fxqxl   0/1     ContainerCreating   0          84s
my-release-harbor-notary-signer-6df446c656-krdvf   0/1     ContainerCreating   0          84s
my-release-harbor-portal-dc4f56754-q2c8r           0/1     ContainerCreating   0          84s
my-release-harbor-redis-0                          0/1     ContainerCreating   0          75s
my-release-harbor-registry-c4d5564bd-bbxf9         0/2     ContainerCreating   0          84s
```

tiller standard_init_linux.go:178: exec user process caused "exec format error"

https://gitlab.com/gitlab-org/gitlab-foss/issues/64044
https://gitlab.com/gitlab-org/gitlab-foss/-/merge_requests/31887
