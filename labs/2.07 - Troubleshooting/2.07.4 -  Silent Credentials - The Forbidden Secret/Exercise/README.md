# 🧰 Lab 3.09.4 - Silent Credentials: The Forbidden Secret

## 🎯 Scenario

You’re deploying a secure application that needs access to sensitive data through Kubernetes Secrets. You've configured the necessary RBAC and mounted the secret both as a volume and through environment variables. The application pod starts—but logs indicate that it cannot access the secret data.

---

## 🧭 Step-by-step

1. Apply all manifests in the scenario directory
```bash
kubectl apply -f namespace.yaml
kubectl apply -f service-account.yaml
kubectl apply -f secret.yaml
kubectl apply -f deployment.yaml
```

2. Check pod status and logs
3. Investigate why the application can't access secrets

---

## 🏁 Completion checklist

* [ ] Verified the ServiceAccount and its role bindings
* [ ] Confirmed the Role has access to the required resources
* [ ] Checked the Secret and the way it’s referenced in the Deployment
* [ ] Ensured the pod successfully accessed the secret (via logs)