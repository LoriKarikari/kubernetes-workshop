# Lab 1.05 – Services

## Introduction

Your Deployment is running and pods are healthy. But how do other applications—or you—connect to them? Pod IPs are ephemeral and change when pods restart. You need a stable network endpoint.

In Kubernetes, this means **exposing your Deployment** using a **Service**. Services provide a consistent way to access a set of pods, regardless of which specific pods are running at any given time.

## Objectives

- Create a **Kubernetes Service** to expose your Deployment
- Choose the appropriate service type (`ClusterIP`, `NodePort`, or `LoadBalancer`) based on your needs
- Test connectivity to your application through the Service


## Step-by-step: Creating Services

### Phase I: Internal access – ClusterIP + port forwarding

1. **Create a ClusterIP Service manifest**

   Define a YAML file named `webapp-service.yaml` that specifies a `ClusterIP` service to expose your Deployment internally.

2. **Apply the ClusterIP Service**

   Submit the service definition to the cluster.

3. **Verify the Service**

   Confirm that the service is active and has endpoints.

4. **Establish communication via port forwarding**

   Temporarily forward traffic from your machine to the service using:

   ```bash
   kubectl port-forward service/webapp-svc 8080:80
   curl http://localhost:8080
   ```

   This allows you to test the service from your local machine without external exposure.

### Phase II: External access – Upgrade to LoadBalancer

5. **Update the Service to LoadBalancer**

   Edit your existing service file or use the command line to change its type to `LoadBalancer`, making it accessible from outside the cluster.

   Change:

   ```yaml
   type: ClusterIP
   ```

   to:

   ```yaml
   type: LoadBalancer
   ```

   Save and reapply.

6. **Get the external IP**

   Wait for Azure to provision the load balancer and assign an external IP.

7. **Test external access to the LoadBalancer**

   Access your application via the external IP in your browser or with curl.


## Resources

- [Services](https://kubernetes.io/docs/concepts/services-networking/service/)
