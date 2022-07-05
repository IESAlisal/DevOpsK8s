# Authentication and authorization in Kubernetes

## Crear namespace

    kubectl create namespace lfs158
    mkdir rbac
    cd rbac/

## Añado usuario

    sudo useradd -s /bin/bash bob
    sudo passwd bob

## Generar claves

    openssl genrsa -out bob.key 2048
    openssl req -new -key bob.key -out bob.csr -subj "/CN=bob/O=learner"

### Creación del archivo de petición de certificado

    vim signing-request.yaml

Contenido del fichero

```yaml
apiVersion: certificates.k8s.io/v1
kind: CertificateSigningRequest
metadata:
  name: bob-csr
spec:
  groups:
  - system:authenticated
  request: <assign encoded value from next cat command>
  signerName: kubernetes.io/kube-apiserver-client
  usages:
  - digital signature
  - key encipherment
  - client auth
```

## Ver la petición en base64 y asignar el resultado al campo request del fichero de petición

    cat bob.csr | base64 | tr -d '\n','%'
    vim signing-request.yaml    (para modificar el campo request con la salida del cat anterior)

## Crea la petición de certificado. certificate signing request

    kubectl create -f signing-request.yaml
    kubectl get csr
    - La petición todavía está en estado de pendiente

## Aprobación del certificado

    kubectl certificate approve bob-csr
    kubectl get csr
    - La petición de certificado ha sido aprobada

## Extraer el certificado aprobado de la petición de firma de certificado, decodificarlo en base64 y guardarlo en un fichero de certificado .crt

    kubectl get csr bob-csr -o jsonpath='{.status.certificate}' | base64 -d > bob.crt
    cat bob.crt

## Configure the kubectl client's configuration manifest with user bob's credentials by assigning his key and certificate

    kubectl config set-credentials bob --client-certificate=bob.crt --client-key=bob.key

## Create a new context entry in the kubectl client's configuration manifest for user bob, associated with the lfs158 namespace in the minikube cluster

    #kubectl config set-context bob-context --cluster=minikube --namespace=lfs158 --user=bob
    kubectl config set-context bob-context --cluster=minibox --namespace=lfs158 --user=bob    

## Mientras esté en el contexto minikube (yo lo estoy haciendo en el minibox), cree una nueva implementación/deployment en el espacio de nombres lfs158

    kubectl -n lfs158 create deployment nginxjavi  --image=nginx:alpine
    kubectl -n lfs158 create deployment apachejavi --image=httpd:2.4.53 --replicas=3

    #Borrar un deployment $kubectl -n lfs158 delete deployment

## Desde el nuevo contexto bob-context intente enumerar los pods. El intento falla porque el usuario bob no tiene permisos configurados para el contexto bob

    kubectl --context=bob-context get pods

## Asignación de permisos limitados al usuario bob en el bob-context

### Crear a YAML configuration manifest for a pod-reader Role object, which allows only get, watch, list actions/verbs in the lfs158 namespace

    vim role.yaml

Contenido del fichero

``` yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  name: pod-reader
  namespace: lfs158
rules:
- apiGroups: [""]
  resources: ["pods"]
  verbs: ["get", "watch", "list"]
```

### Crear y listar el rol

    kubectl create -f role.yaml
    kubectl -n lfs158 get roles

## Create a YAML configuration manifest for a rolebinding object, which assigns the permissions of the pod-reader Role to user bob. Then create the rolebinding object and list it from the default minikube context, but from the lfs158 namespace

    vim rolebinding.yaml

Contenido del fichero

``` yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: pod-read-access
  namespace: lfs158
subjects:
- kind: User
  name: bob
  apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: Role
  name: pod-reader
  apiGroup: rbac.authorization.k8s.io
```

    kubectl create -f rolebinding.yaml 
    kubectl -n lfs158 get rolebindings

### Desde el nuevo contexto bob-context intente enumerar los pods. Ahora si que funcionará correctamente

    kubectl --context=bob-context get pods
