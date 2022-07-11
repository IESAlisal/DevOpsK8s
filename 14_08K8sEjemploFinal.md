# Ejemplo Ingress

https://redhat-scholars.github.io/kubernetes-tutorial/kubernetes-tutorial/ingress.html

## Habilitar y verificar Ingress

    minikube addons enable ingress -p minibox
    kubectl get pods -n ingress-nginx

## Crear Deployment 1

    kubectl apply -f 14_08K8sEjemploFinalDeploy1.yaml

## Exponer servicio  1

    kubectl expose deployment quarkus-demo-deployment --type=NodePort --port=8080
    kubectl get service quarkus-demo-deployment

    IP=$(minikube ip -p minibox)
PORT=$(kubectl get service/quarkus-demo-deployment -o jsonpath="{.spec.ports[*].nodePort}")
    echo $IP:$PORT

    minikube service list -p minibox
    kubectl get deployments quarkus-demo-deployment
    kubectl get replicasets
    kubectl get deploy,po,svc quarkus-demo-deployment    

## Aplicar ingress

    kubectl apply -f 14_08K8sEjemploFinalIngress1.yaml
    kubectl get ingress

## Registro DNS en /etc/hosts

    sudo bash -c "echo $(minikube ip -p minibox) kube-devnation.info >> /etc/hosts"
    cat /etc/hosts

## Crear deployment 2

    kubectl apply -f 14_08K8sEjemploFinalDeploy2.yaml

## Exponer servicio  2

    kubectl expose deployment mynode-deployment --type=NodePort --port=8080

    kubectl get service mynode-deployment

    IP=$(minikube ip -p minibox)
PORT=$(kubectl get service/mynode-deployment -o jsonpath="{.spec.ports[*].nodePort}")
    echo $IP:$PORT

    minikube service list -p minibox
    kubectl get deployments mynode-deployment
    kubectl get replicasets
    #kubectl get deploy,po,svc mynode-deployment    

## Mofidicar el ingress anterior para añadir un nuevo PATH /v2

    #####TODO Este comando parece que no funciona #####
    kubectl apply -f 14_08K8sEjemploFinalIngress2.yaml
