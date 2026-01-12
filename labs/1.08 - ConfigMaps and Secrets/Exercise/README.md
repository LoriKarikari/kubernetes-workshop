## Lab 1.08 - ConfigMaps & Secrets

## Introduction

Hardcoding configuration values inside container images is inflexible and insecure. What happens when you need different settings for dev vs. production? What about sensitive credentials that shouldn't be in your codebase?

Kubernetes solves this with **ConfigMaps** for general configuration and **Secrets** for sensitive data. Both can be injected into your pods as environment variables or mounted as files—without rebuilding your images.

## Objectives

- Create a **ConfigMap** for general application settings
- Create a **Secret** to store sensitive data (e.g., API keys, passwords)
- Mount these into pods as environment variables
- Confirm that the pods are reading the injected configuration

## Step-by-step: Adding Configuration via ConfigMaps & Secrets

### Phase I: Define configuration resources

**1. Create a ConfigMap**

Create a manifest file `frontend-config.yaml` containing these data fields:

- `LOG_LEVEL`: `debug`
- `CACHE_ENABLED`: `true`

**2. Create a Secret**

Create a manifest file `frontend-secrets.yaml` containing the following sensitive data:

- `apiKey`: `my-secret-api-key`
- `dbPassword`: `Zzhbwkkjikh123`

(Hint: these values must be base64 encoded)


### Phase II: Update the Deployment to use the configuration

**3. Modify your Deployment**

Update your existing `frontend-deployment.yaml` so the pods receive the above values via **environment variables**.

The following variable names should be configured in your container spec:

| Env Var         | Source                            |
|-----------------|-----------------------------------|
| `LOG_LEVEL`     | From ConfigMap key `LOG_LEVEL`    |
| `CACHE_ENABLED` | From ConfigMap key `CACHE_ENABLED`|
| `API_KEY`       | From Secret key `apiKey`          |
| `DB_PASSWORD`   | From Secret key `dbPassword`      |
| `APP_MOTD`      | From plain text value in manifest |


### Phase III: Deploy and verify

**4. Apply the ConfigMap and Secret to the cluster**

**5. Apply the updated Deployment**

**6. Verify configuration inside the Pods**

Use `kubectl exec` and `printenv` to inspect the injected values:

```bash
kubectl get pods
kubectl exec -it <pod-name> -- printenv | grep LOG
kubectl exec -it <pod-name> -- printenv | grep DB_PASSWORD
```

---

## Resources

- [ConfigMaps](https://kubernetes.io/docs/concepts/configuration/configmap/)
- [Secrets](https://kubernetes.io/docs/concepts/configuration/secret/)
