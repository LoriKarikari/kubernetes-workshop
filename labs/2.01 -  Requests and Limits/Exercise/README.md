# Lab 2.01 - Resource Requests & Limits

## Introduction

In this lab, you'll configure **resource requests and limits** for containers within a **Deployment**. These settings help the scheduler make intelligent placement decisions and prevent any single workload from starving others.

## Objectives

- Define **CPU and memory requests and limits** in your deployment spec
- Ensure lightweight workloads operate with appropriate resource allocations
- Create a heavier `backend` deployment to reflect higher capacity requirements
- Observe the behavior of the scheduler when a pod requests more resources than available

## Step-by-step: Configuring Resource Policies

### Step 01: Update `frontend.yaml`

Edit the frontend deployment file. Update the container spec to include resource requests and limits:

```yaml
resources:
  requests:
    cpu: "100m"
    memory: "64Mi"
  limits:
    cpu: "200m"
    memory: "128Mi"
```

This ensures the containers declare their expected resource usage and cannot exceed their assigned budget.

### Step 02: Apply and Inspect

1. Apply the updated Deployment
2. Check the Deployment and Pods
3. Use `kubectl describe pod <pod-name>` and review the `Limits` and `Requests` sections to verify proper settings


### Step 03: Add a Backend Deployment

Create a new deployment file called `backend-deployment.yaml` for a heavier workload (e.g., a database or API server that needs more resources).

Apply the manifest and confirm the pod is scheduled with its enhanced allocation.

### Step 04: Test Overconsumption

1. Create a test pod (`overload-pod`) without any resource limits and monitor its usage
2. Try requesting more than the available node capacity (e.g., `10000m` CPU), and observe scheduling behavior

The pod should either be **evicted**, **throttled**, or **remain Pending**, depending on the scenario.

## Resources

- [Resource Management for Pods and Containers](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/)