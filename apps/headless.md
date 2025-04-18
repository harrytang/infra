# Headless

Go to the headless directory and run the following command to create the sealed secret:

```bash
export APP_KEYS="$(openssl rand -base64 16),$(openssl rand -base64 16),$(openssl rand -base64 16),$(openssl rand -base64 16)"
export API_TOKEN_SALT="$(openssl rand -base64 16)"
export ADMIN_JWT_SECRET="$(openssl rand -base64 16)"
export JWT_SECRET="$(openssl rand -base64 16)"
export TRANSFER_TOKEN_SALT="$(openssl rand -base64 16)"
export CF_ACCESS_SECRET="toBeReplaced"
export SMTP_PASSWORD="toBeReplaced"
export DATABASE_PASSWORD="toBeReplaced"
export NAMESPACE="toBeReplaced"
kubectl create secret generic --dry-run=client \
    headless-env \
    --namespace=$NAMESPACE \
    --from-literal=APP_KEYS=$APP_KEYS \
    --from-literal=API_TOKEN_SALT=$API_TOKEN_SALT \
    --from-literal=ADMIN_JWT_SECRET=$ADMIN_JWT_SECRET \
    --from-literal=JWT_SECRET=$JWT_SECRET \
    --from-literal=TRANSFER_TOKEN_SALT=$TRANSFER_TOKEN_SALT \
    --from-literal=CF_ACCESS_SECRET=$CF_ACCESS_SECRET \
    --from-literal=SMTP_PASSWORD=$SMTP_PASSWORD \
    --from-literal=DATABASE_PASSWORD=$DATABASE_PASSWORD \
    -o yaml \
    | kubeseal --format=yaml > sealed-secret.yaml
```
