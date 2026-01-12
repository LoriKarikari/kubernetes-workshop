# Lab 1.01 - Imperative Commands

Sometimes you need to act quickly—no time to craft manifests or YAML files. In real-world scenarios like debugging, quick tests, or exam situations, the ability to deploy and manage resources with a few typed commands is invaluable.

In this exercise, you will **use only imperative `kubectl` commands** to complete the tasks. No YAML files, just direct, immediate action.


## Step-by-step: Complete the tasks using imperative commands

1. Deploy a pod named `nginx` using the `nginx:alpine` image

2. Deploy a pod named `redis` with image `redis:alpine` and label `tier=db`

3. Create a ClusterIP service named `redis-service` to expose redis on port 6379

4. Create a deployment named `webapp` using the image `busybox` with 3 replicas. What do you spot when checking the deployment `webapp`? Do you know why?

5. Create a pod named `custom-nginx` using the `nginx` image, exposing container port 8080

6. Create a namespace named `dev-ns`

7. Create a deployment named `redis-deploy` in namespace `dev-ns` using image `redis` with 2 replicas

8. Create a pod named `httpd` using the image `httpd:alpine` in the `default` namespace and expose it as a ClusterIP service named `httpd` targeting port 80 (as few steps as possible)

9. Create a pod interactively named `curl` using the image `curlimages/curl:latest` in the `default` namespace, and curl the httpd pod

🧾 **Expected output**: <Your Answer>

10. Generate a YAML file for a deployment named `nginx-deploy` using image `nginx`, without creating it

11. Restart the `webapp` deployment to simulate a redeploy scenario

12. Scale the `webapp` deployment to 5 replicas

13. Port forward traffic from your local machine (port 8080) to the httpd service (port 80). What do you see when you access `http://localhost:8080`?

🔗 Then access:
[http://localhost:8080](http://localhost:8080)
🧾 You'll see the default Apache web page from the `httpd` pod.

14. Create a ConfigMap named `app-config` with the following key-value pairs:
    * `ENV=prod`
    * `LOG_LEVEL=debug`

15. Create a Secret named `db-secret` with:
    * `username=admin`
    * `password=supersecret123`

## Resources

- [kubectl reference](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands)