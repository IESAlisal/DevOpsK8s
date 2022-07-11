# Create a Secret from a Definition Manifest

We can create a Secret manually from a YAML definition manifest. The example manifest below is named mypass.yaml. There are two types of maps for sensitive information inside a Secret: data and stringData.

With data maps, each value of a sensitive information field must be encoded using base64. If we want to have a definition manifest for our Secret, we must first create the base64 encoding of our password:

## secret data

$ echo mysqlpassword | base64

bXlzcWxwYXNzd29yZAo=

and then use it in the definition manifest. Archivo **mypass.yaml**:

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: my-password
type: Opaque
data:
  password: bXlzcWxwYXNzd29yZAo=
```

    kubectl create -f mypass.yaml

## Secret StringData

Archivo definition manifest. Archivo **mypass.yaml**:

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: my-password
type: Opaque
stringData:
  password: mysqlpassword
```

    kubectl create -f mypass.yaml

## Crear Secreto desde un fichero

    echo mysqlpassword | base64
        bXlzcWxwYXNzd29yZAo=
    echo -n 'bXlzcWxwYXNzd29yZAo=' > password.txt

Now we can create the Secret from the password.txt file:

    kubectl create secret generic my-file-password --from-file=password.txt
    kubectl get secret my-file-password
    kubectl describe secret my-file-password

## Use Secrets Inside Pods: As Environment Variables

Secrets are consumed by Containers in Pods as mounted data volumes, or as environment variables, and are referenced in their entirety or specific key-values.

Below we reference only the **password** key of the **my-password** Secret and assign its value to the **WORDPRESS_DB_PASSWORD** environment variable:

```yaml
....
spec:
  containers:
  - image: wordpress:4.7.3-apache
    name: wordpress
    env:
    - name: WORDPRESS_DB_PASSWORD
      valueFrom:
        secretKeyRef:
          name: my-password
          key: password
....
```
