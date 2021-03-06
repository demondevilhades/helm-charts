# nas-apps

My app chart on qnap k3s.

![nas-k3s](https://github.com/demondevilhades/helm-charts/blob/main/static/nas-k3s.png?raw=true)

## See
`
https://github.com/demondevilhades/helm-charts/tree/main/nas/apps/nas-apps
`

## app & ports

| Type  | App  | NodePort  |
|:--------|:------|:----------|
| Ops    | speedtest    | 61010    |
| Ops    | wetty    | 61020    |
| Def    | dashboard    | 61060    |
| Tool    | qbittorrent    | 61100    |
| Tool    | proxy    | 61110    |
| Game    | tm    | 61200    |
| Game    | ag    | 61210    |

## Ops

### adolfintel/speedtest


### wettyoss/wetty


## Tool

### linuxserver/qbittorrent


### proxy


## Game

### ltdstudio/terraforming-mars


### awkward_guests


## run

### volume dependency
```
kubernetes create ns app

helm install -n app nfs-app ./nas-nfs \
    --set fullnameOverride=nfs-app \
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

helm uninstall -n app nfs-app
```

### start/update/stop
```

helm upgrade --install -n app nas-apps ./nas-apps \
--set wetty.ssh.ip={host.ip} \
--set ag.create=true

helm uninstall -n app nas-apps
```
