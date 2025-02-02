# How to upgrade kubernetes cluster

## Solution

[Upgrade Document](https://v1-31.docs.kubernetes.io/docs/tasks/administer-cluster/kubeadm/upgrading-linux-nodes/)

I have used KindCli/Tools which help me to run this pratice on my local machine. How to use kind please follow this [link](https://github.com/nomansadiq11/devops-utils/blob/main/mac/kindcli.md).

You can create multinode cluster with specfic verion and then you can run your upgrade excersize on it


```bash

# remove existing kubeadm, which probbly installed using binary
rm $(which kubeadm)

# update repo with kubeadm version like 1.30 cluster running
apt-get update
apt-get install -y apt-transport-https ca-certificates curl gpg
curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.30/deb/Release.key |  gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.30/deb/ /' |  tee /etc/apt/sources.list.d/kubernetes.list
apt-get update

# Install kubeadm
apt-get install -y kubeadm

# for upgrade, you need to change the repo to upgraded verion like here I added 1.31

curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.31/deb/Release.key |  gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.31/deb/ /' |  tee /etc/apt/sources.list.d/kubernetes.list


```

[Follow this document to upgrade it ](https://v1-31.docs.kubernetes.io/docs/tasks/administer-cluster/kubeadm/upgrading-linux-nodes/)

> or run below script on earch node 

```bash
# replace x in 1.31.x-* with the latest patch version
apt-mark unhold kubeadm && \
apt-get update && apt-get install -y kubeadm='1.31.1-*' && \
apt-mark hold kubeadm



apt-mark unhold kubelet kubectl && \
apt-get update && apt-get install -y kubelet='1.31.1-*' kubectl='1.31.1-*' && \
apt-mark hold kubelet kubectl

systemctl daemon-reload
systemctl restart kubelet



```