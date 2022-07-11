# Create a Secret from Literal Values

## Crear un secreto para una contraseña de mysql

    kubectl create secret generic my-password --from-literal=password=mysqlpassword

    kubectl get secret my-password
    kubectl describe secret my-password
    kubectl get secret my-password -o yaml
    kubectl get secret my-password -o json
