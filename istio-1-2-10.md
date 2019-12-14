```
Image:         docker.io/istio/citadel:1.2.10
Image:         docker.io/istio/galley:1.2.10
Image:         docker.io/istio/kubectl:1.2.10
Image:         docker.io/istio/mixer:1.2.10
Image:         docker.io/istio/pilot:1.2.10
Image:         docker.io/istio/proxyv2:1.2.10
Image:         docker.io/istio/sidecar_injector:1.2.10
Image:         docker.io/jaegertracing/all-in-one:1.9
Image:         docker.io/prom/prometheus:v2.8.0
Image:         quay.io/kiali/kiali:v0.20
Image:         docker.io/istio/proxy_init:1.2.10
```
```
cat sh  | grep harbor.test.com | awk '{print "docker pull "$1":"$2}' | sh
docker load -i istio-1-2-10-allinone.tar
```
```
  docker tag    istio/citadel:1.2.10   docker.io/istio/citadel:1.2.10
  docker tag    istio/galley:1.2.10  docker.io/istio/galley:1.2.10
  docker tag    istio/kubectl:1.2.10  docker.io/istio/kubectl:1.2.10
  docker tag    istio/mixer:1.2.10  docker.io/istio/mixer:1.2.10
  docker tag     istio/pilot:1.2.10 docker.io/istio/pilot:1.2.10
  docker tag    istio/proxyv2:1.2.10   docker.io/istio/proxyv2:1.2.10
  docker tag     istio/sidecar_injector:1.2.10 docker.io/istio/sidecar_injector:1.2.10
  docker tag     prom/prometheus:v2.8.0 docker.io/prom/prometheus:v2.8.0
  docker tag     jaegertracing/all-in-one:1.9 docker.io/jaegertracing/all-in-one:1.9
  docker tag     kiali/kiali:v0.20  quay.io/kiali/kiali:v0.20
  docker tag    istio/proxy_init:1.2.10 docker.io/istio/proxy_init:1.2.10
```
