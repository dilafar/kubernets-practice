### create key pair

    openssl genrsa -out dev-tom.key 2048

### create certificate signing request

    openssl req -new -key dev-tom.key -subj "/CN=tom" -out dev-tom.csr

### get the base64 encoded value of csr

    cat dev-tom.csr | base64 | tr -d "\n"

### send csr to k8s certificate api

    kubectl apply -f dev-tom-csr.yaml

### view csr

    kubectl get csr

### approve csr

    kubectl certificate approve dev-tom.csr

### get signed certificate

    kubectl get csr dev-tom -o yaml

### get options

    kubectl options

### connect to cluster

    kubectl --server={api-server-address} \
    --certificate-authority=/etc/kubernetes/pki/ca.crt \
    --client-certificate=dev-tom.crt \
    --client-key=dev-tom.key \
    get pods

### check user permission

    kubectl auth can-i get pod —-as {user-name}

### create service account

    kubectl create service account jenkins

### connect to cluster

    kubectl --server $server \
    --certificate-authority /etc/kubernetes/pki/ca.crt \
    --token $token \
    --user jenkins \
    get pods

### check serviceaccount permission

    kubectl auth can-i create service --as system:serviceaccount:default:jenkins
