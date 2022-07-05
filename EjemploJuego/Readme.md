# DOSBOX IN A CONTAINER WITH VNC CLIENT

[https://github.com/theonemule/dos-game](https://github.com/theonemule/dos-game)

Yo lo he probado con ubuntu 22.04

## Crear y conectar

To connect use this, first create a file called keen.yaml file, configure your instance kubectl to work with your instance of Kubernetes, then run deploy the sample.

    kubectl create -f keen.yaml

## Para ver la URL

    minikube service --all -p minibox