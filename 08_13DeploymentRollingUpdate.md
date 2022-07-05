# Deployment of the application. Rolling Update and Rollback

    kubectl create deployment mynginx --image=nginx:1.15-alpine
    kubectl get deployments

## Mostrar todos los deployments, replicasets y pods

    kubectl get deploy,rs,po -l app=mynginx
    kubectl get pods -o wide

## Aumentar el número de replicas de la apliación

    kubectl scale deploy mynginx --replicas=3
    kubectl get deploy,rs,po -l app=mynginx

## "Describir" el deployment

    kubectl describe deployment mynginx

## Estado e Historial del deployment. Roolout

    kubectl rollout status deployment mynginx
    kubectl rollout history deployment mynginx
    (Inicialmente tiene una única versión. 1)

    - Revisar el historial de la versión 1
    kubectl rollout history deployment mynginx --revision=1

## Actualizar el deployment con una nueva imagen

    kubectl set image deployment mynginx nginx=nginx:1.16-alpine
    kubectl rollout history deployment mynginx --revision=2
    kubectl get deploy,rs,po -l app=mynginx

    - Uno de los replicasets ha pasado a 0 el número de pods ejecutandose.

## Actualizar otra vez el deployment con una nueva imagen

    kubectl set image deployment mynginx nginx=nginx:1.21.6-alpine
    kubectl rollout history deployment mynginx --revision=3
    kubectl get deploy,rs,po -l app=mynginx

    - Dos de los replicasets han pasado a 0 el número de pods ejecutandose.

### Miro el estado

    kubectl rollout status deployment mynginx

### Miro el historial

    kubectl rollout history deployment mynginx

## Rollback a la versión 1

    kubectl rollout undo deployment mynginx --to-revision=1
    kubectl rollout history deployment mynginx
    kubectl get deploy,rs,po -l app=mynginx

    - El replicaset ha regresado a su estado original.
    - Se genera un nuevo número de versión. Ahora tengo la versión 2 y la 3

    (Parece que se puede hacer hasta 10 rollbacks)
