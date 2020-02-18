```
www.beginswithdata.com › 2017-06-23-fsck-k8s
```
pod 反亲和性
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
```
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: redis-failover
        component: sentinel
        creator: redisfailover
        redisfailover: os-redis
        sentinel: os-redis
    spec:
      affinity:
        nodeAffinity:
          preferredDuringSchedulingIgnoredDuringExecution:
          - preference:
              matchExpressions:
              - key: nodeType
                operator: In
                values:
                - controller
            weight: 100
        podAntiAffinity:
          preferredDuringSchedulingIgnoredDuringExecution:
          - podAffinityTerm:
              labelSelector:
                matchLabels:
                  app: redis-failover
                  component: sentinel
                  creator: redisfailover
                  redisfailover: os-redis
                  sentinel: os-redis
              topologyKey: kubernetes.io/hostname
            weight: 100

   

```

```

kubectl patch deployment patch-demo --patch "$(cat patch-file-containers.yaml)"

spec:
  template:
    spec:
      containers:
      - name: patch-demo-ctr-2
        image: redis
```
