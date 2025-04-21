# Remark42

## Condig map

```bash
kubectl create configmap email-templates \
  --from-file=email_confirmation_login.html.tmpl \
  --from-file=email_confirmation_subscription.html.tmpl \
  --from-file=email_reply.html.tmpl \
  --from-file=email_unsubscribe.html.tmpl \
  --from-file=error_response.html.tmpl \
  --dry-run=client -o yaml > email-templates.config-map.yaml
```

## Apple Key

```bash
kubectl -n $NAMESPACE create secret generic apple-key --from-file=apple.p8 --dry-run=client -o yaml | kubeseal --format=yaml > apple-key.sealed-secret.yaml
```

## Sealed secrets

```bash
export NAMESPACE="toBeReplaced"
export AUTH_TWITTER_CID="toBeReplaced"
export AUTH_TWITTER_CSEC="toBeReplaced"
export AUTH_GOOGLE_CID="toBeReplaced"
export AUTH_GOOGLE_CSEC="toBeReplaced"
export AUTH_GITHUB_CID="toBeReplaced"
export AUTH_GITHUB_CSEC="toBeReplaced"
export AUTH_FACEBOOK_CID="toBeReplaced"
export AUTH_FACEBOOK_CSEC="toBeReplaced"
export AUTH_APPLE_CID="toBeReplaced"
export AUTH_APPLE_TID="toBeReplaced"
export AUTH_APPLE_KID="toBeReplaced"
export TELEGRAM_TOKEN="toBeReplaced"
export SECRET=$(openssl rand -base64 32)
export SMTP_USERNAME="toBeReplaced"
export SMTP_PASSWORD="toBeReplaced"

kubectl create secret generic --dry-run=client \
    remark42-env \
    --namespace=$NAMESPACE \
    --from-literal=AUTH_TWITTER_CID=$AUTH_TWITTER_CID \
    --from-literal=AUTH_TWITTER_CSEC=$AUTH_TWITTER_CSEC \
    --from-literal=AUTH_GOOGLE_CID=$AUTH_GOOGLE_CID \
    --from-literal=AUTH_GOOGLE_CSEC=$AUTH_GOOGLE_CSEC \
    --from-literal=AUTH_GITHUB_CID=$AUTH_GITHUB_CID \
    --from-literal=AUTH_GITHUB_CSEC=$AUTH_GITHUB_CSEC \
    --from-literal=AUTH_FACEBOOK_CID=$AUTH_FACEBOOK_CID \
    --from-literal=AUTH_FACEBOOK_CSEC=$AUTH_FACEBOOK_CSEC \
    --from-literal=AUTH_APPLE_CID=$AUTH_APPLE_CID \
    --from-literal=AUTH_APPLE_TID=$AUTH_APPLE_TID \
    --from-literal=AUTH_APPLE_KID=$AUTH_APPLE_KID \
    --from-literal=TELEGRAM_TOKEN=$TELEGRAM_TOKEN \
    --from-literal=SECRET=$SECRET \
    --from-literal=SMTP_USERNAME=$SMTP_USERNAME \
    --from-literal=SMTP_PASSWORD=$SMTP_PASSWORD \
    -o yaml \
    | kubeseal --format=yaml > sealed-secret.yaml
```
