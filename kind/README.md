# kind
kind 让你能够在本地计算机上运行 Kubernetes。 kind 要求你安装并配置好 Docker

# Install
[Link](https://kind.sigs.k8s.io/docs/user/quick-start/#installation)

### On Linux
```bash
curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.10.0/kind-linux-amd64
chmod +x ./kind
mv ./kind /some-dir-in-your-PATH/kind
```

### On Mac
``` bash
brew install kind
```
or
``` bash
curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.10.0/kind-darwin-amd64
```

# Useful commands
1. Create k8s cluster
``` bash
kind create cluster # Default cluster context name is `kind`.
...
kind create cluster --name kind-2
```

2. List cluster manager by kind
``` bash
kind get clusters
```

3. update node kind-control-plane with then label 'ingress-ready' and then value 'true'
``` bash
kubectl label node kind-control-plane ingress-ready=true
```