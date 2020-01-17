```
  minio/minio:latest
  minio/mc:latest
  velero/velero:v1.1.0 
```

```



创建 minio 的访问密钥文件 credentials-velero
cat <<'EOF' > credentials-velero
[default]
aws_access_key_id = minio
aws_secret_access_key = minio123
EOF

cp velero /usr/local/bin/
velero install \
    --image velero/velero:v1.1.0 \
    --provider aws \
    --bucket velero \
    --namespace velero \
    --secret-file ./credentials-velero \
    --velero-pod-cpu-request 200m \
    --plugins velero/velero-plugin-for-aws:v1.0.0
    --velero-pod-mem-request 200Mi \
    --velero-pod-cpu-limit 1000m \
    --velero-pod-mem-limit 1000Mi \
    --use-volume-snapshots=false \
    --use-restic \
    --restic-pod-cpu-request 200m \
    --restic-pod-mem-request 200Mi \
    --restic-pod-cpu-limit 1000m \
    --restic-pod-mem-limit 1000Mi \
    --backup-location-config region=minio,s3ForcePathStyle="true",s3Url=http://{minio_service_ip}:31489

kubectl get crd|grep velero    
```
