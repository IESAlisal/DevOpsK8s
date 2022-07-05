# Liveness

## Prueba liveness

    Ejecuta una prueba que verifica cada 5 segundos el estado de un contenedor a partir del archivo /tmp/healthy
    Luego borra el archivo /tmp/healthy y se espera que reinicie el contenedor de nuevo automáticamente

    kubectl create -f 11_13liveness.yaml

    kubectl get pod liveness-exec -w

    kubectl describe pod liveness-exec

## Salida del log de prueba

  Warning  Unhealthy  100s (x4 over 4m55s)   kubelet            Liveness probe failed: cat: can't open '/tmp/healthy': No such file or directory
  Normal   Killing    100s (x4 over 4m55s)   kubelet            Container liveness failed liveness probe, will be restarted
  Normal   Pulling    5s (x6 over 5m29s)     kubelet            Pulling image "k8s.gcr.io/busybox"