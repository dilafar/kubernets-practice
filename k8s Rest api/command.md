### useful links

    Access Cluster using API: https://kubernetes.io/docs/tasks/administer-cluster/access-cluster-api/
    Programmatic Access: https://kubernetes.io/docs/tasks/administer-cluster/access-cluster-api/#programmatic-access-to-the-api
    Client Libraries: https://kubernetes.io/docs/reference/using-api/client-libraries/
    api-groups: https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.28/

### set API SERVER Endpoint

    SERVER=https://172.31.44.88:6443

### set Token var

    kubectl get serviceaccount myscript -o yaml
    kubectl get secret xxxxx -o yaml

    TOKEN=$(echo "token" | base64 --decode | tr -d "\n")

### certificate base connection

    curl -X GET $SERVER/api --header "Authorization: Bearer $TOKEN" --cacert /etc/kubernetes/pki/ca.crt

### non certificate base connection

    curl -X GET $APISERVER/api --header "Authorization: Bearer $TOKEN" --insecure

### main endpoint

    curl -X GET $SERVER/api --header "Authorization: Bearer $TOKEN" --cacert /etc/kubernetes/pki/ca.crt

### List all deployments in default namespace

    curl -X GET $SERVER/apis/apps/v1/namespaces/default/deployments --header "Authorization: Bearer $TOKEN" --cacert /etc/kubernetes/pki/ca.crt

### List all services in default namespace

    curl -X GET $SERVER/api/v1/namespaces/default/services --header "Authorization: Bearer $TOKEN" --cacert /etc/kubernetes/pki/ca.crt

### get specific service

    curl -X GET $SERVER/api/v1/namespaces/default/services/nginx-service --header "Authorization: Bearer $TOKEN" --cacert /etc/kubernetes/pki/ca.crt

### get all pod names

    curl -X GET $SERVER/api/v1/namespaces/default/pods/pod-name/logs --header "Authorization: Bearer $TOKEN" --cacert /etc/kubernetes/pki/ca.crt
