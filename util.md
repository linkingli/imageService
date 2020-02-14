```
www.beginswithdata.com › 2017-06-23-fsck-k8s
```
```
        selector:
            matchLabels:
               app: xxx
      在template里：添加
          podAntiAffinity:
          preferredDuringSchedulingIgnoredDuringExecution:
          - podAffinityTerm:
              labelSelector:
                matchLabels:
                 app: xxx
              topologyKey: kubernetes.io/hostname
            weight: 100

```
