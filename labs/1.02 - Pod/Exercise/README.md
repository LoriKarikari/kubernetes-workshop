# Lab 1.02 - Create a Pod

## Introduction

In this lab, you'll create your first pod using a YAML manifest and learn the basic commands to manage it.

## Objectives

- Connect to your Kubernetes cluster using `kubectl`
- Define a pod manifest in YAML
- Deploy a single pod into the cluster
- Monitor its status and confirm it's running

## Step-by-step: Deploying a Pod

### Step 01: Define the Pod manifest

Create a YAML file named `my-first-pod.yaml` that describes your pod's metadata and container image (`nginx`).

### Step 02: Apply the Pod manifest to the cluster

Use `kubectl` to submit your pod definition to the cluster:

```bash
kubectl apply -f my-first-pod.yaml
```

### Step 03: Verify the Pod is running

Confirm that your pod has successfully started:

```bash
kubectl get pods
```

For more details:

```bash
kubectl describe pod my-first-pod
```

Check the logs:

```bash
kubectl logs my-first-pod
```

## Resources

- [Pods](https://kubernetes.io/docs/concepts/workloads/pods/)

