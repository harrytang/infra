# GitOps

## Sealed Secrets

### Namespace

```bash
export NAMESPACE='harrytang-{prod,staging}'
```

### Signing Key

```bash
kubectl create secret generic fluxcd-signing-key \
  --namespace $NAMESPACE \
  --dry-run=client -o yaml \
  --from-file=./git.asc | \
  kubeseal --format=yaml > ./fluxcd-signing-key.sealed-secret.yaml
```

### Slack URL

```bash
export SLACK_URL=https://hooks.slack.com/services/XXX/YYY/ZZZZ
kubectl create secret generic slack-url \
  --namespace $NAMESPACE \
  --dry-run=client -o yaml \
  --from-literal=address=$SLACK_URL | \
  kubeseal --format=yaml > ./slack-url.sealed-secret.yaml
```
