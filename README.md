# kubernetes-fleet

## Requisites
Before you starte please install docker on your host!

## K3D

```
.
├── dev-cluster-121.conf
├── dev-cluster-122.conf
├── dev-cluster-123.conf
├── dev-cluster-124.conf
├── dev-cluster.conf
├── dev-cluster-no-lb.conf
├── dev-cluster-custom.conf
├── dev-cluster-cks.conf
├── prod-cluster.conf
└── stage-cluster.conf

```

***dev-cluster***: 	  1x control plane + 1x worker node<br>
***dev-cluster-no-lb***:  1x control plane + 1x worker node<br>
***dev-cluster-custom***: 1x control plane + 3x worker node with istio onboarded<br>
***stage-cluster***: 	  1x control plane + 4x worker node<br>
***prod-cluster***:       3x control plane + 5x worker node<br>
***dev-cluster-121***:    1x control plane + 3x worker node<br>
***dev-cluster-122***:    1x control plane + 3x worker node<br>
***dev-cluster-123***:    1x control plane + 3x worker node<br>
***dev-cluster-124***:    1x control plane + 3x worker node<br>
***dev-cluster-cks***:    1x control plane + 1x worker node<br>

### Installation

```console
curl -s https://raw.githubusercontent.com/k3d-io/k3d/main/install.sh | bash
```

### Create K3D clusters

*dev:*
```console
k3d cluster create --config=./k3d/dev-config.yaml
```

*dev-custom (istio):*
```console
k3d cluster create --config=./k3d/dev-config-custom.yaml
```

*test:*
```console
k3d cluster create --config=./k3d/stage-config.yaml
```

*prod:*
```console
k3d cluster create --config=./k3d/prod-config.yaml
```

If you need use specific version please visit [here](./K3D-VERSIONS.md)

### Create K3D cluster using utils 
By default dev-cluster will be created although not given cluster name!

**Create:**
```bash
$ ./utils/k3d-wrapper.sh -c
🔥 Creating Kubernetes Cluster: dev-cluster \
✅ Cluster: dev-cluster sucessfully created
```

**List:**
```bash
$ ./utils/k3d-wrapper.sh -l
👍 Cluster: dev-cluster exist!
---------------------------------------------
NAME          SERVERS   AGENTS   LOADBALANCER
dev-cluster   1/1       3/3      true
---------------------------------------------
```

**Delete:**
```bash
$ ./utils/k3d-wrapper.sh -d
⚡ Cluster: dev-cluster exists and will be deleted /
✅ Cluster: dev-cluster sucessfully deleted
```

**Unexisting config file:**
```bash
$ ./utils/k3d-wrapper.sh -c pprod-cluster
👀 Kubernetes cluster config: pprod-cluster.conf does not exist! Please check k3d dir! 
```

#### Deploy cluster with particular configuration
Below configuration contains istio deployment. Be patient this process
can take a while!

```
$ ./utils/k3d-wrapper.sh -c dev-cluster-custom
🔥 Creating Kubernetes Cluster: dev-cluster-custom |
✅ Cluster: dev-cluster-custom sucessfully created

$ ./utils/k3d-wrapper.sh -l dev-cluster-custom
👍 Cluster: dev-cluster-custom exist!
---------------------------------------------
NAME                 SERVERS   AGENTS   LOADBALANCER
dev-cluster-custom   1/1       3/3      true
---------------------------------------------

$ kubectl get ns | grep -i istio
istio-ingress     Active   76s
istio-system      Active   76s

$ kubectl get po -n kube-system
NAME                                      READY   STATUS      RESTARTS   AGE
local-path-provisioner-84bb864455-mh5p9   1/1     Running     0          2m11s
coredns-96cc4f57d-62mmn                   1/1     Running     0          2m11s
metrics-server-ff9dbcb6c-gjdpf            1/1     Running     0          2m11s
helm-install-istio-base--1-nfkfg          0/1     Completed   0          2m11s
helm-install-istio-ingress--1-7frv8       0/1     Completed   0          2m11s
helm-install-istiod--1-nrwcm              0/1     Completed   0          2m11s
```



---

## KIND

```
.
├── dev-config-1c-1w.yaml
├── prod-config-3c-3w.yaml
└── stage-config-1c-2w.yaml
```

***dev***: 1x control plane + 1x worker node<br>
***stage***: 1x control plane + 2x worker node<br>
***prod***: 3x control plane + 3x worker node<br>

### Installation
```
curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.12.0/kind-linux-amd64
sudo chmod +x ./kind
sudo mv ./kind /usr/local/bin/kind
```

### Create KIND clusters

*dev:*
```
kind create cluster --config=./kind/dev-config-1c-1w.yaml
```

*test:*
```
kind create cluster --config=./kind/stage-config-1c-2w.yaml
```

*prod:*
```
kind create cluster --config=./kind/prod-config-3c-3w.yaml
```
