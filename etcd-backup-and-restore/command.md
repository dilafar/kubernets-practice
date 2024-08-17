### install etcdctl

    sudo apt install etcd-client

### backup

    sudo ETCDCTL_API=3 etcdctl snapshot save /tmp/etcd-backup.db \
    --cacert /etc/kubernetes/pki/etcd/ca.crt \
    --cert /etc/kubernetes/pki/etcd/server.crt \
    --key /etc/kubernetes/pki/etcd/server.key

### check backup directory

    ls /tmp/etcd-backup.db

### snapshot status

    sudo ETCDCTL_API=3 etcdctl snapshot status /tmp/etcd-backup.db  --write-out=table

### restore

    sudo ETCDCTL_API=3 etcdctl snapshot restore /tmp/etcd-backup.db  --data-dir /var/lib/etcd-backup

### configure etcd maifiest file to /var/lib/etcd-backup

    vim /etc/kubernetes/manifests/etcd.yaml
