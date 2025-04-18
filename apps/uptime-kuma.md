# Uptime Kuma

## Sealed secrets

```bash
export UPTIME_KUMA_DB_PASSWORD="toBeReplaced"

kubectl create secret generic --dry-run=client \
    uptime-kuma-env \
    --namespace=$NAMESPACE \
    --from-literal=UPTIME_KUMA_DB_PASSWORD=$UPTIME_KUMA_DB_PASSWORD \
    -o yaml \
    | kubeseal --format=yaml > sealed-secret.yaml
```
