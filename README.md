# kubernetes-fleet

## K3D

```
.
├── dev-config.yaml
├── prod-config.yaml
└── stage-config.yaml
```

***dev***: 1x control plane + 3x worker node
***stage***: 1x control plane + 4x worker node
***prod***: 3x control plane + 5x worker node

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

---

## KIND

```
.
├── dev-config-1c-1w.yaml
├── prod-config-3c-3w.yaml
└── stage-config-1c-2w.yaml
```

***dev***: 1x control plane + 1x worker node
***stage***: 1x control plane + 2x worker node
***prod***: 3x control plane + 3x worker node

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
