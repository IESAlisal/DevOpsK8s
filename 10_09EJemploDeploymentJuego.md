# Deployment Juego MSDOS

    https://github.com/theonemule/dos-game
    kubectl create deployment deploy-keen --image=blaize/keen --port=80 --replicas=3
    kubectl create deployment deploy-keen --image=javiteran/mydosbox:latest --port=80 --replicas=3

## Exponer DEPLOYMENT (NodePort)

    kubectl expose deployment deploy-keen --type=NodePort

Verificar y mostrar: Deploymetn, PODs, servicio y endpoints

    kubectl get deploy,po,svc,ep -l app=deploy-keen --show-labels

Ejecuto para ver los servicios y sus URLs:

    minikube service --all -p minibox

    ???kubectl edit deployments.apps deploy-keen

## Borrar

    kubectl delete services deploy-keen
    kubectl delete deployment deploy-keen
