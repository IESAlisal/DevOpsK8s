# ClusterIP y NodePort (simple Pod o deployment)

## Exponer un simple pod via ClusterIP y NodePort como servicio

    kubectl run pod-hello --image=pbitty/hello-from:latest --port=80 --expose=true
    kubectl get po,svc,ep --show-labels

    [https://github.com/pbitty/hello-from](https://github.com/pbitty/hello-from)

Este pod está creado internamente y no expone nada al exterior y minikube no da ninguna URL para acceder a ese servicio en el cluster.

## Para mostrar sólo el selector

    kubectl describe svc pod-hello | grep -i selector

## Para mostrar la IP

    kubectl describe pod pod-hello 
    kubectl describe pod pod-hello | grep -i IP

## Listar los servicios

    minikube service --all -p minibox

## Acceder al servicio desde dentro por ssh/curl

    curl IP

En el ejemplo realizado y ejecutándolo varias veces:
    docker@minibox:~$ curl 10.244.1.2
    Hello from pod-hello (10.244.1.2)docker@minibox:~$ curl 10.244.1.2
    Hello from pod-hello (10.244.1.2)docker@minibox:~$ curl 10.244.1.2
    Hello from pod-hello (10.244.1.2)docker@minibox:~$ curl 10.244.1.2

o con la IP obtenida de kubectl get svc --show-labels)

    kubectl get svc --show-labels
    curl 10.107.242.74

    docker@minibox:~$ curl 10.107.242.74
    Hello from pod-hello (10.244.1.2)docker@minibox:~$ curl 10.107.242.74
    Hello from pod-hello (10.244.1.2)docker@minibox:~$ curl 10.107.242.74

## (Sin SSH se puede obtener el archivo de configuración del servicio)

    kubectl edit svc pod-hello

Esa línea edita el fichero de configuración con el "vi".
Debemos Modificar type=ClusterIP  por NodePort para acceder desde el exterior

## Probar

    kubectl get po,svc,ep --show-labels

Ya sale NodePort y un PORT(s) externo

    minikube service --all -p minibox

Ahora SI se ve un vínculo para acceder al servicio y obtener el mensaje "Hello from POD XXXXXX"

    http://192.168.49.2:31004
