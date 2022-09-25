# nas-apps

My app chart on qnap k3s.

| Type  | App  | NodePort  |
|:--------|:------|:----------|
| Ops    | speedtest    | 61010    |
| Ops    | wetty    | 61020    |
| Def    | dashboard    | 61060    |
| Tool    | qbittorrent    | 61100    |
| Tool    | proxy    | 61110    |
| Tool    | jackett    | 61120    |
| Tool    | nas-tools    | 61130    |
| Game    | tm    | 61200    |
| Game    | ag    | 61210    |

## Ops

### adolfintel/speedtest


### wettyoss/wetty


## Tool

### linuxserver/qbittorrent
Set `Downloads\PreAllocation=false`.
Due to the nfs lock.

### proxy

### jackett
manual config

### nas-tools
manual config
jackett_url: http://jackett:9117
qbittorrent_url: qbittorrent-http:61100

## Game

### ltdstudio/terraforming-mars


### awkward_guests


## run

### volume dependency
```
kubectl create ns app

helm install -n app nas-nfs ./nas-nfs \
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

helm uninstall -n app nas-nfs
```

### start/update/stop
```

helm upgrade --install -n app nas-apps ./nas-apps \
# --set ag.create=true \
--set wetty.ssh.ip={host.ip}

helm uninstall -n app nas-apps
```



