```
Image:         docker.io/istio/citadel:1.3.6
Image:         docker.io/istio/galley:1.3.6
Image:         docker.io/istio/kubectl:1.3.6
Image:         docker.io/istio/mixer:1.3.6
Image:         docker.io/istio/pilot:1.3.6
Image:         docker.io/istio/proxyv2:1.3.6
Image:         docker.io/istio/sidecar_injector:1.3.6
Image:         docker.io/jaegertracing/all-in-one:1.14
Image:         docker.io/prom/prometheus:v2.8.0
Image:         grafana/grafana:6.1.6
Image:         quay.io/kiali/kiali:v1.4
Image:         docker.io/istio/proxy_init:1.3.6
```

```
  docker tag    istio/citadel:1.3.6   docker.io/istio/citadel:1.3.6
  docker tag    istio/galley:1.3.6  docker.io/istio/galley:1.3.6
  docker tag    istio/kubectl:1.3.6  docker.io/istio/kubectl:1.3.6
  docker tag    istio/mixer:1.3.6  docker.io/istio/mixer:1.3.6
  docker tag     istio/pilot:1.3.6 docker.io/istio/pilot:1.3.6
  docker tag    istio/proxyv2:1.3.6   docker.io/istio/proxyv2:1.3.6
  docker tag     istio/sidecar_injector:1.3.6 docker.io/istio/sidecar_injector:1.3.6
  docker tag     prom/prometheus:v2.8.0 docker.io/prom/prometheus:v2.8.0
  docker tag     jaegertracing/all-in-one:1.14 docker.io/jaegertracing/all-in-one:1.14
  docker tag     kiali/kiali:v1.4  quay.io/kiali/kiali:v1.4
  docker tag    istio/proxy_init:1.3.6 docker.io/istio/proxy_init:1.3.6

```
```
docker 

docker.io/istio/citadel:1.3.6
docker.io/istio/galley:1.3.6
docker.io/istio/proxyv2:1.3.6
docker.io/istio/proxy_init:1.3.6
docker.io/prom/prometheus:v2.8.0
docker.io/istio/pilot:1.3.6
docker.io/istio/mixer:1.3.6
docker.io/istio/kubectl:1.3.6
quay.io/kiali/kiali:v1.4
docker.io/jaegertracing/all-in-one:1.14
grafana/grafana:6.1.6


docker.io/istio/proxy_init:1.3.6


harbor:
    Image:         os-harbor-svc.default.svc.cloudos:11443/helm/grafana/grafana:6.1.6
    Image:         os-harbor-svc.default.svc.cloudos:11443/helm/docker.io/istio/citadel:1.3.6
    Image:         os-harbor-svc.default.svc.cloudos:11443/helm/docker.io/istio/galley:1.3.6
    Image:         os-harbor-svc.default.svc.cloudos:11443/helm/docker.io/istio/pilot:1.3.6
    Image:         os-harbor-svc.default.svc.cloudos:11443/helm/docker.io/istio/mixer:1.3.6
    Image:         os-harbor-svc.default.svc.cloudos:11443/helm/docker.io/istio/sidecar_injector:1.3.6
    Image:         os-harbor-svc.default.svc.cloudos:11443/helm/docker.io/istio/proxyv2:1.3.6
    Image:         os-harbor-svc.default.svc.cloudos:11443/helm/docker.io/jaegertracing/all-in-one:1.14
    Image:         os-harbor-svc.default.svc.cloudos:11443/helm/quay.io/kiali/kiali:v1.4
    Image:         os-harbor-svc.default.svc.cloudos:11443/helm/docker.io/prom/prometheus:v2.8.0


docker tag docker.io/istio/citadel:1.3.6  os-harbor-svc.default.svc.cloudos:11443/helm/docker.io/istio/citadel:1.3.6
docker tag docker.io/istio/galley:1.3.6  os-harbor-svc.default.svc.cloudos:11443/helm/docker.io/istio/galley:1.3.6
docker tag docker.io/istio/proxyv2:1.3.6  os-harbor-svc.default.svc.cloudos:11443/helm/docker.io/istio/proxyv2:1.3.6
docker tag  docker.io/prom/prometheus:v2.8.0  os-harbor-svc.default.svc.cloudos:11443/helm/docker.io/prom/prometheus:v2.8.0
docker tag  docker.io/istio/pilot:1.3.6  os-harbor-svc.default.svc.cloudos:11443/helm/docker.io/istio/pilot:1.3.6
docker tag  docker.io/istio/mixer:1.3.6  os-harbor-svc.default.svc.cloudos:11443/helm/docker.io/istio/mixer:1.3.6
docker tag  docker.io/istio/kubectl:1.3.6   os-harbor-svc.default.svc.cloudos:11443/helm/docker.io/istio/kubectl:1.3.6
docker tag    quay.io/kiali/kiali:v1.4  os-harbor-svc.default.svc.cloudos:11443/helm/quay.io/kiali/kiali:v1.4
docker tag   docker.io/jaegertracing/all-in-one:1.14  os-harbor-svc.default.svc.cloudos:11443/helm/docker.io/jaegertracing/all-in-one:1.14
docker tag  grafana/grafana:6.1.6  os-harbor-svc.default.svc.cloudos:11443/helm/grafana/grafana:6.1.6
docker tag docker.io/istio/proxy_init:1.3.6 os-harbor-svc.default.svc.cloudos:11443/helm/docker.io/istio/proxy_init:1.3.6  


docker push   os-harbor-svc.default.svc.cloudos:11443/helm/docker.io/istio/citadel:1.3.6
docker push   os-harbor-svc.default.svc.cloudos:11443/helm/docker.io/istio/galley:1.3.6
docker push    os-harbor-svc.default.svc.cloudos:11443/helm/docker.io/istio/proxyv2:1.3.6
docker push   os-harbor-svc.default.svc.cloudos:11443/helm/docker.io/prom/prometheus:v2.8.0
docker push   os-harbor-svc.default.svc.cloudos:11443/helm/docker.io/istio/pilot:1.3.6
docker push  os-harbor-svc.default.svc.cloudos:11443/helm/docker.io/istio/mixer:1.3.6
docker push   os-harbor-svc.default.svc.cloudos:11443/helm/docker.io/istio/kubectl:1.3.6
docker push  os-harbor-svc.default.svc.cloudos:11443/helm/quay.io/kiali/kiali:v1.4
docker push  os-harbor-svc.default.svc.cloudos:11443/helm/docker.io/jaegertracing/all-in-one:1.14
docker push  os-harbor-svc.default.svc.cloudos:11443/helm/grafana/grafana:6.1.6
docker push   os-harbor-svc.default.svc.cloudos:11443/helm/docker.io/istio/proxy_init:1.3.6 

```
