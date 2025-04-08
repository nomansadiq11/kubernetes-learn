# How todo Pod Taint and Toleration

Use kind create kubernetes cluster locally [link](https://github.com/nomansadiq11/devops-utils/blob/main/mac/kindcli.md).

```shell
kubectl taint node test-control-plane app=test:NoSchedule
```

Create pod, this will only to create that specfic node which has following taint

```yaml

apiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
  tolerations:
  - effect: NoSchedule
    key: app
    value: test
  containers:
  - name: nginx
    image: nginx
    imagePullPolicy: IfNotPresent

```