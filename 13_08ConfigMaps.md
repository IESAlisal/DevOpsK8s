# ConfigMaps

## Creación de un ConfigMap con un archivo html como parámetro

    kubectl create configmap green-web-cm --from-file=13_08index.html

## Verificación de la creación del ConfigMap

    kubectl describe cm green-web-cm

## Creo un deployment basado en el archivo 13_08web-green-with-ConfigMaps.yaml

    kubectl apply -f 13_08web-green-with-ConfigMaps.yaml
    (Borrar) kubectl delete -n default deployment green-web

## Exponer el deploymen con NodePort

    kubectl expose deployment green-web --type=NodePort
    (Borrar)   kubectl delete -n default service green-web

## Listar los servicios publicados

    minikube service list -p minibox

## Ver resultado final de la web con curl y el navegador

    Como he llamado al archivo index.html --> 13_08index.html, entonces tengo que ponerlo en la URL
    Es simplemente por tener los archivos ordenados

    curl -s http://192.168.49.2:31454/13_08index.html | head -4
    o en el navegador
    http://192.168.49.2:31454/13_08index.html