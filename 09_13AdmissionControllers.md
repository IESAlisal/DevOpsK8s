# Getting Started with Admission Controllers (Demo)

    #kubectl -n kube-system describe pod kube-apiserver-minikube | grep -i admission
    kubectl -n kube-system describe pod kube-apiserver-minibox | grep -i admission

## Acceso SSH al cluster. Se puede acceder a cada uno de los nodos

    minikube ssh -p minibox
    minikube ssh -p minibox -n m02
    minikube ssh -p minibox -n m03

    docker ps
