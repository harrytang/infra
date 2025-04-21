# Web

Go to the `web` directory and run the following command to create the sealed secret:

```bash
export NAMESPACE="toBeReplaced"
export CF_API_TOKEN="toBeReplaced"
export REVALIDATE_TOKEN="toBeReplaced"
export ALGOLIA_API_KEY="toBeReplaced"
kubectl create secret generic --dry-run=client \
    web-env \
    --namespace=$NAMESPACE \
    --from-literal=CF_API_TOKEN=$CF_API_TOKEN \
    --from-literal=REVALIDATE_TOKEN=$REVALIDATE_TOKEN \
    --from-literal=ALGOLIA_API_KEY=$ALGOLIA_API_KEY \
    -o yaml \
    | kubeseal --format=yaml > sealed-secret.yaml
```

Staging Authentication

```bash
USER=<USERNAME_HERE>; PASSWORD=$(openssl rand -base64 32); echo "${USER}:$(openssl passwd -stdin -apr1 <<< ${PASSWORD})" >> auth
kubectl -n harrytang-staging create secret generic basic-auth --from-file=auth --dry-run=client -o yaml | kubeseal --format=yaml > basic-auth.sealed-secret.yaml
```
