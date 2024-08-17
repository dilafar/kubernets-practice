### version to upgrade

    sudo apt update
    sudo apt-cache madison kubeadm

### upgrade master

    sudo apt-mark unhold kubeadm && \
    sudo apt-get update && sudo apt-get install -y kubeadm='1.31.x-*' && \
    sudo apt-mark hold kubeadm

### check kubeadm version

    kubeadm version

### get upgrade preview

    sudo kubeadm upgrade plan

### upgrade cluster

    sudo kubeadm upgrade apply v1.31.x

### drain the node

    kubectl drain master --ignore-daemonsets

### upgrade kubelet & kubectl

    sudo apt-mark unhold kubelet kubectl && \
    sudo apt-get update && sudo apt-get install -y kubelet='1.31.x-*' kubectl='1.31.x-*' && \
    sudo apt-mark hold kubelet kubectl

### restart kubelet

    sudo systemctl daemon-reload
    sudo systemctl restart kubelet

### uncordon node

    kubectl uncordon master

### upgrade worker node

    sudo apt-mark unhold kubeadm && \
    sudo apt-get update && sudo apt-get install -y kubeadm='1.31.x-*' && \
    sudo apt-mark hold kubeadm

    sudo kubeadm upgrade node

    kubectl drain worker1 --ignore-daemonsets --force

    sudo apt-mark unhold kubelet kubectl && \
    sudo apt-get update && sudo apt-get install -y kubelet='1.31.x-*' kubectl='1.31.x-*' && \
    sudo apt-mark hold kubelet kubectl

    sudo systemctl daemon-reload
    sudo systemctl restart kubelet

    kubectl uncordon worker1

### document link

    https://kubernetes.io/docs/tasks/administer-cluster/kubeadm/kubeadm-upgrade/
