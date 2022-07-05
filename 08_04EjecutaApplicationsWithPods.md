# Ejecutar aplicaciones en Pods

    kubectl apply -f 08_04nginx_a.yaml

    kubectl get pods

    kubectl get pods -o wide

## Crear por comando el archivo yaml para luego poder ejecutarlo

    kubectl run 0804nginxb --image=nginx --port=88 --dry-run=client -o yaml > 08_04nginx_b.yaml

### Ejecutar la aplicación

    kubectl apply -f 08_04nginx_b.yaml

### Reemplazar la aplicación

    kubectl replace --force -f 08_04nginx_b.yaml

## Ejecutar aplicación sin archivo .yaml

    kubectl apply -f 08_04nginx_b.yaml

## Ver la configuración de los pods en ejecución

    kubectl describe pods
    kubectl apply -f 08_04nginx_b.yaml

## Borrar aplicaciones

    kubectl delete -f 08_04nginx_a.yaml
    kubectl delete pods 0804nginxb
    kubectl delete pods 0804nginxc firstrun

    kubectl get pods -o wide

## Deployments

    kubectl get deployments
