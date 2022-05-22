# nas-nfs

Fork from [NFS subdir external provisioner](https://github.com/kubernetes-sigs/nfs-subdir-external-provisioner) .

## See
`
https://github.com/demondevilhades/helm-charts/tree/main/nas/nfs/nas-nfs
`

## install
```
helm install -n nfs nfs-provisioner ./nfs-subdir-external-provisioner \
    --set fullnameOverride=nfs-01 \
    --set image.repository=demondevilhades/k8s.gcr.io_sig-storage_nfs-subdir-external-provisioner \
    --set serviceAccount.create=false \
    --set nfs.server=awesome-nas \
    --set nfs.path=/data/workspace/docker/data \
    --set nfs.mountOptions="{vers=4}" \
    --set nfs.storage=1000Gi \
    --set storageClass.name=sc-nfs-app \
    --set storageClass.provisionerName=nfs-app \
    --set storageClass.reclaimPolicy=Retain \
    --set storageClass.accessModes=ReadWriteMany
```
