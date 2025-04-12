# How to use Cilium and Create the Polices

Use kind create kubernetes cluster locally [link](https://github.com/nomansadiq11/devops-utils/blob/main/mac/kindcli.md).

Follow Cilium [Link](https://docs.cilium.io/en/stable/installation/kind/)

```yaml
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
- role: control-plane
- role: worker
- role: worker
- role: worker
networking:
  disableDefaultCNI: true

```

Still in progress....