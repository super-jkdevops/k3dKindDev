# Different k3s images

| NR  | K3S VERSION   | K3D CONFIG                                     | 
|-----|---------------|------------------------------------------------|
| 1   | 1.21.11+k3s1  | [dev-config-121.yaml](k3d/dev-config-121.yaml) |
| 2   | 1.22.8+k3s1   | [dev-config-122.yaml](k3d/dev-config-122.yaml) |
| 3   | v1.23.5+k3s1  | [dev-config-123.yaml](k3d/dev-config-123.yaml) |

### Example usage
```console


$ kubectl get no -o=custom-columns=NAME:.metadata.name,VERSION:.status.nodeInfo.kubeletVersion
NAME                           VERSION
k3d-dev-cluster-121-agent-0    v1.21.11+k3s1
k3d-dev-cluster-121-server-0   v1.21.11+k3s1

$ kubectl get no -o=custom-columns=NAME:.metadata.name,VERSION:.status.nodeInfo.kubeletVersion
NAME                           VERSION
k3d-dev-cluster-122-agent-0    v1.22.8+k3s1
k3d-dev-cluster-122-server-0   v1.22.8+k3s1

$ kubectl get no -o=custom-columns=NAME:.metadata.name,VERSION:.status.nodeInfo.kubeletVersion
NAME                           VERSION
k3d-dev-cluster-123-server-0   v1.23.5+k3s1
k3d-dev-cluster-123-agent-0    v1.23.5+k3s1

```