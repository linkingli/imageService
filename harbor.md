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
