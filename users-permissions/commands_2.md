### create key pair

    openssl genrsa -out dev-tom.key 2048

### create certificate signing request

    openssl req -new -key dev-tom.key -subj "/CN=tom/O=dev" -out dev-tom.csr

### create crt

    sudo openssl x509 -req -in dev-tom.csr -CAcreateserial -CA /etc/kubernetes/pki/ca.crt -CAkey /etc/kubernetes/pki/ca.key -out dev-tom.crt -days 1000

## create kubeconfig file

### Set the cluster info

    kubectl --kubeconfig=dev.config config set-cluster devcluster \
    --certificate-authority=/etc/kubernetes/pki/ca.crt \
    --server=$SERVER \
    --embed-certs=true

### Set the user credentials

    kubectl --kubeconfig=dev.config config set-credentials tom \
    --client-certificate=dev-tom.crt \
    --client-key=dev-tom.key \
    --embed-certs=true

### Set the context

    kubectl --kubeconfig=dev.config config set-context tom@devcluster \
    --cluster=devcluster \
    --user=tom \
    --namespace=dev

### Use the context

    kubectl --kubeconfig=dev.config config use-context tom@devcluster

### create namespace dev

    kubectl create namespace dev

### create role

    kubectl create role dev-service --verb=get,list,create,delete --resource=pods -n dev --dry-run=client -o yaml > dev-service-role.yaml

### create role binding

    kubectl create rolebinding dev-service-rb -n dev --user=tom --role=dev-service --dry-run=client -o yaml >dev-service-rb.yaml

### test config

    kubectl --kubeconfig dev.config -n dev get pods
