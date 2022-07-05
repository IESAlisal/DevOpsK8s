# Managing Node Applications with DaemonSets

El DaemonSet es utilizado para monitorización, logging, networking, proxies, etc.

[https://kubernetes.io/docs/concepts/workloads/controllers/daemonset](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset)
La documentación muestra la creación de un Daemonset que simplificaremos.

En cada nodo del cluster se ejecutará una réplica del pod definido en el archivo 08_15DaemonSetsFluentdAgent.yaml

## Creando el DaemonSet

    kubectl apply -f 08_15DaemonSetsFluentdAgent.yaml
    
    (Veo que está en el namesapce kube-system)
    kubectl get daemonset.apps -A
    


    (Tengo un poco de lio por ver en que cluster se están instalando las aplicaciones. Nginx y fluentd-agent
    Con el comando siguiente veo TODOS los namespaces y en que NODO del cluster está cada cosa.))
    kubectl get pods -A -o wide
    kubectl get pods -n kube-system -o wide

    kubectl get ds -A

## Borrado de dameonsets

    kubectl delete ds fluentd-agent -n kube-system

    kubectl get ds -A
