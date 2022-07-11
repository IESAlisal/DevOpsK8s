# ConfigMaps

## Creación de un ConfigMap con un archivo html como parámetro

    kubectl create configmap web-azul-cm --from-file=index.html

## Verificación de la creación del ConfigMap

    kubectl describe cm web-azul-cm

## Creo un deployment basado en el archivo web-azul.yaml

    kubectl apply -f web-azul.yaml

## Exponer el deploymen con NodePort

    kubectl expose deployment web-azul --type=NodePort

## Listar los servicios publicados

    minikube service list -p minibox

## Ver resultado final de la web con curl y el navegador

    curl -s http://192.168.49.2:32044| head -4
    o en el navegador
    http://192.168.49.2:32044

## Forzar cambio en ingress

    kubectl replace --force web-azul.yaml
