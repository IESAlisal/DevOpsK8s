# Ejemplo Ingress

https://redhat-scholars.github.io/kubernetes-tutorial/kubernetes-tutorial/ingress.html

## Habilitar y verificar Ingress

    minikube addons enable ingress -p minibox
    kubectl get pods -n ingress-nginx

## Crear Deployment

    kubectl apply -f 15_01WordPressDeploy.yaml

## Exponer servicio

    kubectl expose deployment wordpress-ies-alisal --type=NodePort --port=8082
    kubectl get service wordpress-ies-alisal

    IP=$(minikube ip -p minibox)
PORT=$(kubectl get service/wordpress-ies-alisal -o jsonpath="{.spec.ports[*].nodePort}")
    echo $IP:$PORT

    minikube service list -p minibox
    kubectl get deployments wordpress-ies-alisal
    kubectl get replicasets
    kubectl get deploy,po,svc wordpress-ies-alisal    

## Aplicar ingress

    kubectl apply -f 15_01WordPressIngress.yaml
    kubectl get ingress

## Registro DNS en /etc/hosts

    sudo bash -c "echo $(minikube ip -p minibox) wp.iesalisal.es >> /etc/hosts"
    cat /etc/hosts

