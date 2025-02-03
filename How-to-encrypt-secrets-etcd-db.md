# How to encrypt secrets etcd db

## Reason

- You need to encrypt your data at rest, so whatever secrets we creates in kubernetes it's store in etcd DB. If somehow your database hacked you need to make sure your secrets are encrypted
- So you can enable the encryption at rest by using `EncryptionConfiguration`

## Solution

kubernetes documentations
[https://kubernetes.io/docs/tasks/administer-cluster/encrypt-data/](https://kubernetes.io/docs/tasks/administer-cluster/encrypt-data/)
[https://kubernetes.io/docs/tasks/administer-cluster/encrypt-data/](https://kubernetes.io/docs/tasks/administer-cluster/encrypt-data/)

- Create this yaml in controlplane
- Add this to KubeAPI server in configuration `--encryption-provider-config=file-location-path` add `volume` and `volumemount`

```yaml

---
apiVersion: apiserver.config.k8s.io/v1
kind: EncryptionConfiguration
resources:
  - resources:
      - secrets
    providers:
      - aescbc:
          keys:
            - name: key1
              secret:  aGVsbG8gd29ybGQ= ## this is base64 encoded (hello world) key of
      - identity: {}

```

> create new secret and validate it by calling etcdctl api to see the data (look for documentations)