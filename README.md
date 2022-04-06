# kubernetes-fleet

## Requisites
Before you starte please install docker on your host!

## K3D

```
.
├── dev-config.yaml
├── prod-config.yaml
└── stage-config.yaml
```

***dev***: 1x control plane + 3x worker node<br>
***stage***: 1x control plane + 4x worker node<br>
***prod***: 3x control plane + 5x worker node<br>

### Installation

```
curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.12.0/kind-linux-amd64
sudo chmod +x ./kind
sudo mv ./kind /usr/local/bin/kind
```

### Create K3D clusters

*dev:*
```
k3d cluster create --config=./k3d/dev-config.yaml
```

*test:*
```
k3d cluster create --config=./k3d/stage-config.yaml
```

*prod:*
```
k3d cluster create --config=./k3d/prod-config.yaml
```

If you need use specific version please visit [here](./K3D-VERSIONS.md)

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
curl -s https://raw.githubusercontent.com/k3d-io/k3d/main/install.sh | bash
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
