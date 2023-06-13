# Deploying a Stand-AloneApplication using CLI

## Borrar deployment anterior y sus replicasets

    kubectl delete deployments web-dash
    kubectl get replicasets
    kubectl get pods

## Crear archivo 11_10webserver.yaml

``` yaml
    apiVersion: apps/v1
    kind: Deployment
    metadata:
    name: webserver
    labels:
        app: nginx
    spec:
    replicas: 3
    selector:
        matchLabels:
        app: nginx
    template:
        metadata:
        labels:
            app: nginx
        spec:
        containers:
        - name: nginx
            image: nginx:alpine
            ports:
            - containerPort: 80
```

## Crear deployment

    kubectl create -f 11_10webserver.yaml

## Revisar configuración con el dashboard y CLI

    kubectl get dec
    kubectl describe pod web-dash-74d8bd488f-dwbzz

## Mostrar mas datos del pod con dos columnas nuevas

    kubectl get pods -L app,label2

Filtro por selector. Recupera nuestros pods con app nginx
    kubectl get pods -l app=nginx

Filtro con otro selector. No recupera ningun pod
    kubectl get pods -l k8s-app=webserver

## Exposing an application usando el fichero 11_10webserver.yaml. Crear servicio expuesto Nodeport

    kubectl create -f 11_10webserver-svc.yaml
ó este
    kubectl expose deployment webserver --name=web-service --type=NodePort

## ver servicio expuesto

    kubectl get services

## Detalles del servicio

    kubectl describe service web-service

## Acceder a la aplicación

La aplicación se ejecuta en el minikube VM node. Primero hay que recuperar la IP de la VM minikube minibox

    minikube ip

Abrimos el navegador con el puerto expuesto por el servicio y la ip de la VM minikube minibox y se verá la página de nginx
    http://192.168.49.2:30629/

## Comando minikube service web-service

We could also run the following minikube command which displays the application in our browser:

    minikube service web-service

Opening kubernetes service default/web-service in default browser...

We can see the Nginx welcome page, displayed by the webserver application running inside the Pods created. Our requests could be served by either one of the three endpoints logically grouped by the Service since the Service acts as a Load Balancer in front of its endpoints.

## Mirar todos los servicios ejecutados y su URL

    minikube service --all -p minibox
