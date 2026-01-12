# Lab 1.03 - Create a Deployment

## Introduction

A single pod is fine for learning, but real workloads need reliability and scalability. What happens if your pod crashes? What if you need to handle more traffic?

A **Deployment** solves these problems by managing multiple identical pods, ensuring a desired number of replicas are always running, and providing self-healing capabilities.

## Objectives

- Create a Kubernetes Deployment that launches multiple pods
- Ensure the deployment is declarative, replicable, and self-healing
- Scale the deployment up or down as needed
- Monitor and validate the health and operational readiness of all pods

## Step-by-step: Creating a Deployment

### Step 01: Define the Deployment manifest

Create a YAML file (e.g., `webapp-deployment.yaml`) that specifies the desired number of pods, the container image, and basic metadata.

### Step 02: Apply the Deployment to the cluster

Use `kubectl` to submit the deployment to your cluster.

### Step 03: Verify the Deployment is running

Ensure your pods have launched and are running.

### Step 04: Scale the Deployment

Increase capacity by editing the deployment:

```bash
kubectl edit deployment webapp
```

This opens the deployment manifest in your default editor (usually `vi` or `nano`).

🔍 Locate this section:

```yaml
spec:
  replicas: 3
```

✏️ Change it to:

```yaml
spec:
  replicas: 10
```

### Step 05: Observe self-healing in action

Terminate a pod manually to simulate a failure:

```bash
kubectl delete pod <pod-name>
```

Watch Kubernetes automatically replace it.

## Resources

- [Deployments](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)
