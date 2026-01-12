# Lab 1.00 - Provisioning AKS with Azure CLI

## Overview

In this lab, you'll set up an Azure Kubernetes Service (AKS) cluster from scratch using the Azure CLI.

## Objectives

1. Use the **Azure CLI** to create a new **AKS cluster**
2. Configure it with **Workload Identity** for secure identity delegation
3. Enable **OIDC issuer** and **managed identity**
4. Deploy into a designated **resource group** and region

## Step-by-step instructions

### Step 01: Define the base parameters

Choose and declare your configuration:

- Resource Group: `rg-aks-workshop`
- AKS Cluster Name: `aks-workshop-cluster`
- Location: `francecentral`
- Node Size: `Standard_D4ads_v6`
- Node Count: `2`
- Enable OIDC issuer and workload identity

```bash
export RESOURCE_GROUP="rg-aks-workshop"
export CLUSTER_NAME="aks-workshop-cluster"
export LOCATION="francecentral"
export NODE_SIZE="Standard_D4ads_v6"
```

```bash
# Create the resource group
az group create \
  --name $RESOURCE_GROUP \
  --location $LOCATION
```

### Step 02: Deploy the AKS cluster

```bash
az aks create \
  --resource-group $RESOURCE_GROUP \
  --name $CLUSTER_NAME \
  --location $LOCATION \
  --enable-managed-identity \
  --enable-oidc-issuer \
  --node-vm-size $NODE_SIZE \
  --node-count 2 \
  --enable-cluster-autoscaler \
  --min-count 1 \
  --max-count 5 \
  --node-osdisk-size 64 \
  --generate-ssh-keys
```

### Step 03: Add a high-performance node pool with ephemeral OS disks

Add an extra node pool for workloads needing fast local storage (e.g., CI runners, caching layers):

```bash
az aks nodepool add \
  --resource-group $RESOURCE_GROUP \
  --cluster-name $CLUSTER_NAME \
  --name userpool \
  --node-count 1 \
  --node-vm-size $NODE_SIZE \
  --node-osdisk-type Ephemeral \
  --node-osdisk-size 64 \
  --mode User
```

### Step 04: Connect to the cluster

```bash
az aks get-credentials \
  --resource-group $RESOURCE_GROUP \
  --name $CLUSTER_NAME
```

Check the cluster status:

```bash
kubectl cluster-info
```

Verify the nodes:

```bash
kubectl get nodes -o wide
```

Check the running pods:

```bash
kubectl get pods -A
```

Check services:

```bash
kubectl get svc -A
```