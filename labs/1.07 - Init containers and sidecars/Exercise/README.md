# Lab 1.07 - Init Containers & Sidecars

## Introduction

Before your main application starts, you often need to run setup tasks—waiting for a database to be ready, fetching configuration, or running migrations. These tasks must complete successfully before the main container starts.

In Kubernetes, this sequence is handled by **Init Containers**, which run to completion before the main workload starts. In parallel, **sidecar containers** run alongside the main container to provide supporting functionality like logging, monitoring, or proxying.

In this lab, you'll enhance the existing **frontend deployment** with:

- An **init container** that performs a simulated startup check
- A **sidecar container** that monitors and logs activity

## Objectives

Modify your existing `frontend-deployment.yaml` manifest to:

- Add an **init container** that writes a startup status file
- Add a **sidecar container** that tails and logs the file
- Share a volume between all containers
- Perform all steps **declaratively** using manifest files


## Step-by-step: Adding Init Containers and Sidecars

1. Open the existing `frontend-deployment.yaml` deployment file.

2. Add a shared volume named `startup-status`.

3. Define an **init container** named `startup-check` that writes to `/var/startup/status.txt`

4. Update the existing `web` container to mount the volume and serve the file from `/usr/share/nginx/html`

5. Add a **sidecar container** named `log-agent` that tails the file

6. Apply the updated deployment

7. Watch the pod rollout and confirm it waits for the init container

8. Confirm that the sidecar logs the startup message


## Resources

- [Init Containers](https://kubernetes.io/docs/concepts/workloads/pods/init-containers/)
- [Sidecar Containers](https://kubernetes.io/docs/concepts/workloads/pods/sidecar-containers/)

