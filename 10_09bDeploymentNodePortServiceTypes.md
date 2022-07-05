# Crear un Deployment con tipo de servicio NodePort

## Crear como DEPLOYMENT con varias réplicas

    kubectl create deployment deploy-hello --image=pbitty/hello-from:latest --port=80 --replicas=3

## Exponer DEPLOYMENT (NodePort)

    kubectl expose deployment deploy-hello --type=NodePort

Verificar y mostrar: Deploymetn, PODs, servicio y endpoints 

    kubectl get deploy,po,svc,ep -l app=deploy-hello --show-labels

Ejecuto para ver los servicios y sus URLs:

    minikube service --all -p minibox

Si abro el link en el explorador van cambiando los endpoints que responden:
    javiteran@ubud21:~/github/IntroK8s$ curl http://192.168.49.2:32283
    Hello from deploy-hello-668f74dc49-5jxz6 (10.244.0.12)javiteran@ubud21:~/github/IntroK8s$ curl http://192.168.49.2:32283
    Hello from deploy-hello-668f74dc49-g2vtr (10.244.1.3)javiteran@ubud21:~/github/IntroK8s$ curl http://192.168.49.2:32283
    Hello from deploy-hello-668f74dc49-ddl5z (10.244.2.2)javiteran@ubud21:~/github/IntroK8s$ curl http://192.168.49.2:32283
    Hello from deploy-hello-668f74dc49-5jxz6 (10.244.0.12)javiteran@ubud21:~/github/IntroK8s$ 