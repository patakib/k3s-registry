# Docker Registry

# Setup
I followed this guide: https://rpi4cluster.com/k3s-docker-registry/ with some modifications.

## Storage Class
I applied the default local-path (see in ```storageClassName``` field in the ```pvc.yaml``` file).
More info: https://docs.k3s.io/storage.  
It will show "Pending" state (you don't need to have a PV), but once a Pod or a Deployment would use it, it will be bound (if it is correctly referred in the Pod manifest - see ```deployment.yaml```).

## Service
I use a ```NodePort``` service because I don't want to expose my cluster and it is enough for the homelab / skill building for me.
Therefore check out ```service.yaml``` and see how it is different to the file on the website link provided.

## Hosts

### /etc/hosts
Put ```127.0.0.1    registry    registry.cube.local``` in the file in a new row.

### /etc/rancher/k3s/registries.yaml
Paste this:  

```
mirrors:
  docker-registry:
    endpoint:
      - "http://registry.cube.local:30500"
```
