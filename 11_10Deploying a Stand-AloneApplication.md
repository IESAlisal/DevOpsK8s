# Deploying a Stand-AloneApplication

## Arrancar servicios

    minikube start -p minibox
    minikube status -p minibox
    minikube dashboard -p minibox

## Crear aplicación con el Dashboard

From there, we can create an application using a valid YAML/JSON configuration data, from a file, or manually from the Create from form tab. Click on the Create from form tab and provide the following application details:

    The application name is web-dash.
    The Docker image to use is nginx.
    The replica count, or the number of Pods, is 1.
    Service is External, Port 8080, Target port 80, Protocol TCP


## Revisar configuración con el dashboard y CLI

    kubectl get deployments
    kubectl get replicasets
    kubectl get pods

## Ver detalles del pod

    kubectl describe pod web-dash-74d8bd488f-dwbzz

## Mostrar mas datos del pod con dos columnas nuevas

    kubectl get pods -L k8s-app,label2

Filtro por selector. Recupera nuestro pod web-dash-74d8bd488f-dwbzz
    kubectl get pods -l k8s-app=web-dash

Filtro con otro selector. No recupera ningun pod
    kubectl get pods -l k8s-app=webserver
