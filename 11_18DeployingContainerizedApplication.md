# 11_18DeployingContainerizedApplication.md

## Crar deployment apache con CLI

    kubectl create deployment web-cli-javi --image=httpd

## mostrar pod, deployment y replicaset

    kubectl get all -l app=web-cli-javi

## Crear otro deployment apache con FICHERO.YAML

    kubectl create -f 11_18web-cli-javi-file.yaml
    kubectl get all -l app=web-cli-javi-file

### Exponer el deployment en un puerto

    ##kubectl expose deployment web-cli-javi --type=LoadBalancer --port=80 --target-port=80
    kubectl expose deployment web-cli-javi --type=NodePort --port=80

    minikube service --all        -p minibox

## Creación de un deployment con el DASHBOARD

    kubectl get all -l k8s-app=web-nginx-dashboard
    
    minikube service --all -p minibox
