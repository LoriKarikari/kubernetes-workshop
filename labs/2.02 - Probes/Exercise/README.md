# Lab 2.02 - Health Probes

## Introduction

In this lab, you'll implement **Kubernetes probes** to ensure your pods are fully operational before they start handling requests.


## Objectives

Deploy a pod with:

- A **Startup Probe** to allow time for slow-starting containers
- A **Liveness Probe** to detect when a container is unhealthy and needs to be restarted
- A **Readiness Probe** to confirm the container is ready to receive traffic

## Step-by-step: Adding Probes

1. Add a `startupProbe`, `livenessProbe`, and `readinessProbe` to the `frontend` deployment
2. Apply the updated deployment
3. Inspect probe status using `kubectl describe`

## Resources

- [Configure Liveness, Readiness and Startup Probes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/)
