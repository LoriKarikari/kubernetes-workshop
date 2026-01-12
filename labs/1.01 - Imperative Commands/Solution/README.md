# Lab 1.01 - Imperative Commands

## Solution

1. Deploy a pod named `nginx` using the `nginx:alpine` image

```bash
kubectl run nginx \
  --image=nginx:alpine
```

2. Deploy a pod named `redis` with image `redis:alpine` and label `tier=db`

```bash
kubectl run redis \
  --image=redis:alpine \
  --labels=tier=db
```

3. Create a ClusterIP service named `redis-service` to expose redis on port 6379
```bash
kubectl expose pod redis \
  --name=redis-service \
  --port=6379 \
  --target-port=6379 \
  --type=ClusterIP
```

4. Create a deployment named `webapp` using the image `busybox` with 3 replicas. What do you spot when checking the deployment `webapp`? Do you know why?
```bash
kubectl create deployment webapp \
  --image=busybox \
  --replicas=3
```

5. Create a pod named `custom-nginx` using the `nginx` image, exposing container port 8080
```bash
kubectl run custom-nginx \
  --image=nginx \
  --port=8080
```

6. Create a namespace named `dev-ns`
```bash
kubectl create namespace dev-ns
```

7. Create a deployment named `redis-deploy` in namespace `dev-ns` using image `redis` with 2 replicas
```bash
kubectl create deployment redis-deploy --image=redis --replicas=2 -n dev-ns
```

8. Create a pod named `httpd` using the image `httpd:alpine` in the `default` namespace and expose it as a ClusterIP service named `httpd` targeting port 80 (as few steps as possible)
```bash
kubectl run httpd \
  --image=httpd:alpine \
  --port=80 \
  --expose
```

9. Create a pod interactively named `curl` using the image `curlimages/curl:latest` in the `default` namespace, and curl the httpd pod

Get the IP address of the `httpd` pod

```bash
kubectl get pod httpd -o wide
```

```bash
kubectl run curl --image=curlimages/curl:latest -it --rm --restart=Never -- curl <HTTPD_POD_IP>
```

🧾 **Expected output**: It works!

1.  Generate a YAML file for a deployment named `stormtrooper` using image `nginx`, without creating it
```bash
kubectl create deployment stormtrooper \
  --image=nginx \
  --dry-run=client \
  -o yaml > stormtrooper.yaml
```

1.  Restart the `webapp` deployment to simulate a redeploy scenario
```bash
kubectl rollout restart deployment webapp
```

1.  Scale the `webapp` deployment to 5 replicas
```bash
kubectl scale deployment webapp --replicas=5
```

1.  Port forward traffic from your local machine (port 8080) to the httpd service (port 80). What do you see when you access `http://localhost:8080`?
```bash
kubectl port-forward service/httpd 8080:80
```

🔗 Then access:
[http://localhost:8080](http://localhost:8080)
🧾 You’ll see the default Apache web page from the `httpd` pod.

14. Create a ConfigMap named `app-config` with the following key-value pairs:

* `ENV=prod`
* `LOG_LEVEL=debug`

```bash
kubectl create configmap app-config --from-literal=ENV=prod --from-literal=LOG_LEVEL=debug
```

15. Create a Secret named `db-secret` with:

* `username=admin`
* `password=imperial123`

```bash
kubectl create secret generic db-secret --from-literal=username=admin --from-literal=password=imperial123
```
