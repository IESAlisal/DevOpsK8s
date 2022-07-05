# Using a Shared hostPath Volume Type

## Creación de un deployment con dos contenedores

    El deployment se hace utilizando el fichero 12_06app-blue-shared-vol.yaml

    kubectl apply -f 12_06app-blue-shared-vol.yaml

## Exponer el deployment en un puerto

    kubectl expose deployment blue-app --type=LoadBalancer --port=80 --target-port=80
    o
    kubectl expose deployment blue-app --type=NodePort 

    kubectl get deploy,po,svc
    minikube service list -p minibox

## Ver lo que muestra la página web en nginx

    curl http://192.168.49.2:31248/