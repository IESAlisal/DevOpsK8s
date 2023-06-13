# Ingress. SERVICIO CLAVE ENLAZADO CON DNS

## Ingress. Verificar deployment

    kubectl get deploy,svc

## Ingress con nginx

Verificar la lista de addons y ver el estado del ingress (deshabilitado)

    minikube addons  list -p minibox
    minikube service list -p minibox

## Habilitar ingress

    minikube addons list -p minibox
    minikube addons enable ingress -p minibox
    minikube addons list -p minibox

## Crear ingress

    kubectl apply -f 14_08Ingress_web-azul_web-verde.yaml
    kubectl get ingress
    kubectl describe ingress ingress-demo

## modificar y verificar el archivo host para añadir IP/Nombre de cada host

    sudo bash -c "echo $(minikube ip -p minibox) version-estable.color.io version-test.color.io >> /etc/hosts"
    cat /etc/hosts
