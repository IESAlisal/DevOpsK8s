# kubectl en Kubernetes

[Página Oficial instalación kubernetes/Kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/)

## Funcionamiento kubectl sin instalar

    minikube kubectl -- get nodes
    minikube kubectl -- get namespaces
    minikube kubectl -- get pods --all-namespaces
    minikube kubectl -- get pods --all-namespaces -o wide

    minikube -p minibox kubectl -- get pods --all-namespaces 

## Download the latest release with the command

    curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"

## Instalación de kubectl

    sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl

## Prueba de instalacion

    kubectl version --client

## Shell autompletion

    sudo apt install -y bash-completion
    source /usr/share/bash-completion/bash_completion
    source <(kubectl completion bash)
    echo "source <(kubectl completion bash)" >> ~/.bashrc

## Ver configuracion

    kubectl config view
    kubectl cluster-info

<https://kubernetes.io/docs/reference/kubectl/>

La cofiguración del minikube está en: /.kube/config

## comandos kubectl

    kubectl get nodes
    kubectl get namespaces
    kubectl get pods --all-namespaces
    kubectl get pods -A 
    kubectl get pods --all-namespaces -o wide

## Kubernetes Dashboard

    minikube addons list
    minikube addons enable metrics-server
    minikube addons enable dashboard
    minikube addons list
    minikube dashboard

    minikube dashboard -p minibox
    (Para ejecutar el dashboard de otro cluster)

## APIs with 'kubectl proxy'

    kubectl proxy
