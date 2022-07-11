# Ingress. SERVICIO CLAVE ENLAZADO CON DNS

## Ingress. Verificar deployment

    kubectl get deploy,svc

## Ingress con nginx

Verificar la lista de addons y ver el estado del ingress (deshabilitado)

    minikube addons list -p minibox
     minikube service list -p minibox

| ingress    | minikube | disabled | unknown (third-party)          |
| ingress-dns| minikube | disabled | google                         |

## Habilitar ingress

    minikube addons enable ingress -p minibox
    minikube addons list -p minibox

## Crear ingress

    kubectl apply -f 14_08Ingress-demoVideo.yaml
    kubectl get ingress
    kubectl describe ingress ingress-demo

## modificar y verificar el archivo host para añadir IP/Nombre de cada host

    sudo bash -c "echo $(minikube ip -p minibox)  blue.example.com >> /etc/hosts"
    sudo bash -c "echo $(minikube ip -p minibox) green.example.com >> /etc/hosts"

    o
    sudo bash -c "echo $(minikube ip -p minibox) blue.example.com green.example.com >> /etc/hosts"
    cat /etc/hosts

## Forzar cambio en ingress

    kubectl replace --force 14_08Ingress-demoVideo.yaml
