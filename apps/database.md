# Database

## Credentials

Root password

```bash
export NAMESPACE="toBeProvided"
export ROOT_PASSWORD="$(openssl rand -base64 32)"
export PASSWORD="$(openssl rand -base64 32)"
kubectl create secret generic --dry-run=client \
    mariadb \
    --namespace=$NAMESPACE \
    --from-literal=password=$PASSWORD \
    --from-literal=root-password=$ROOT_PASSWORD \
    -o yaml \
    | kubeseal --format=yaml > sealed-secret.yaml
```
