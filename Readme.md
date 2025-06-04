Prerequisites:
- развернутый minikube кластер
- настроенный minio с использованием оператора (https://min.io/docs/minio/kubernetes/upstream/operations/installation.html)
- установленный velero, который имеет доступ к бакету minio
```
Пример установки:
    velero install --provider aws \
    --plugins velero/velero-plugin-for-aws:v1.7.0 \
    --bucket velero-bucket \
    --secret-file ./velero-credentials \
    --use-volume-snapshots=false \
    --backup-location-config \
        region=minio \
        s3Url=http://minio-tenant-hl.minio-tenant.svc.cluster.local:9000,\
        s3ForcePathStyle=true,\
        insecureSkipTLSVerify=true
```

! Деплой приложения с помощью k8s:
```
    Запустить kubectl apply -f для всех конфигов внутри папки /k8s
```

! Старт приложения с помощью Docker compose:
```
Первичный запуск
    sudo docker compose run web django-admin startproject composeexample .
```
```
Последующие запуски
    sudo docker compose up
ИЛИ
    sudo docker compose run web
```

Бэкап
- Бэкап файлов БД:
```
    velero backup create db-backup --include-namespaces=db --snapshot-volumes
```
- Проверка статуса бэкапа:
```
    velero backup describe sfs-backup --details
```
