# How todo Pod Node Affinity

Use kind create kubernetes cluster locally [link](https://github.com/nomansadiq11/devops-utils/blob/main/mac/kindcli.md).

```shell
kubectl get nodes --show-labels
```

This will create pod to specfic node group as describe in match expression

```yaml

apiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
  affinity:
    nodeAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
        nodeSelectorTerms:
        - matchExpressions:
          - key: kubernetes.io/os
            operator: In
            values:
            - linux
  containers:
  - name: nginx
    image: nginx
    imagePullPolicy: IfNotPresent

```