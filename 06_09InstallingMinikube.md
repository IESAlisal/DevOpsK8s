# Kubernetes Minikube instalación

Información obtenida del curso de edX

[Edx LinuxFoundation LFS158x. Introduction to Kubernetes:](https://learning.edx.org/course/course-v1:LinuxFoundationX+LFS158x+1T2022/block-v1:LinuxFoundationX+LFS158x+1T2022+type@sequential+block@c77b0dbe0dfe4196be4c88c2c3e43699/block-v1:LinuxFoundationX+LFS158x+1T2022+type@vertical+block@9519e88f3cfd4aa789a4f43d06ae0ddf)

## Comandos de instalación en ubuntu

    curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
    sudo install minikube-linux-amd64 /usr/local/bin/minikube

## Para verificar si está habilitada la virtualización por hardware

    $grep -E --color 'vmx|svm' /proc/cpuinfo

## Parece que se debe administrar sin ser root

    minikube start
    minikube status 
    minikube stop

## Funcionamiento

 Si se instala sobre un docker la propia instalación genera un docker llamado gcr.io/k8s-minikube/kicbase:v0.0.30 que administra y tiene dentro como 10 docker de administración del minikube

Ese docker es el NODO/HOST por defecto del cluster Kubernetes

## Inicia la herramienta KUBEADM

## Verificar el estado del cluster

    minikube profile list

## Nuevo profile minibox con 3 nodos

    minikube start -n 3 -p minibox     (ARRANCAR TAMBIEN EL CLUSTER DE NUEVO?)
    
    minikube status -p minibox
    #(Puedes tener los dos cluster con dos perfiles diferentes arrancados)

## Listar nodos e IPs

    #kubectl get nodes
    minikube node list
    minikube node list -p minibox

    #minikube node list -p minibox | grep -E --color 'Ready|NotReady'

    minikube ip
    minikube ip -p minibox

    minikube -p minibox ip -n minibox-m02

## Borrar perfiles

    minikube delete -p minibox
    minikube delete
