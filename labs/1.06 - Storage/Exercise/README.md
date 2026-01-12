# Lab 1.06 - Persistent Volumes

## Introduction

In this lab, you'll set up storage using Kubernetes **PersistentVolumes (PVs)** and **PersistentVolumeClaims (PVCs)**. These volumes exist independently from your pods, ensuring that data survives pod restarts and redeployments.


## Objectives

- Define a **PersistentVolume (PV)** representing an external storage device
- Create a **PersistentVolumeClaim (PVC)** that binds to the PV
- Deploy a pod that uses the PVC to write data to persistent storage
- Validate that pod restarts do **not** lose data
- Configure dynamic provisioning with Azure Disks (CSI)

## Step-by-step: Deploying Persistent Storage

### Phase I: Define the PersistentVolume

1. Create a `PersistentVolume` named `local-storage-pv` with the following specs:

   - **Storage**: 1Gi
   - **Access Mode**: ReadWriteOnce
   - **Volume Type**: Use `hostPath` (for demo purposes)
   - **Path**: `/tmp/app-data` on the node

### Phase II: Create a PersistentVolumeClaim

2. Define a `PersistentVolumeClaim` named `local-storage-pvc` that requests:

   - **Storage**: 1Gi
   - **Access Mode**: ReadWriteOnce
   - Must match the PV's storage class or leave it unset

### Phase III: Deploy the data logger Pod

3. Create a pod named `data-logger` that:
   - Uses the `busybox` image
   - Mounts the `local-storage-pvc` at `/data`
   - Runs a long sleep or loop so you can inspect it

```
command: ["/bin/sh"]
args: ["-c", "while true; do echo $(date) >> /data/log.txt; sleep 10; done"]
```

### Phase IV: Apply and verify

4. Apply all manifests.

5. Verify that the PVC is **bound** to the PV.

6. Inspect the logs written to the mounted volume:

```bash
kubectl exec data-logger -- cat /data/log.txt
```

### Phase V: Test Pod destruction and persistence

7. Delete and recreate the pod.

8. Confirm that the log file still contains earlier entries—proving that the volume preserved the data.

### Phase VI: Dynamic provisioning with Azure Disks (CSI)

Now you'll integrate Azure Disks using the Container Storage Interface (CSI) for dynamic storage provisioning. This allows you to attach reliable, persistent volumes to pods without manual provisioning.

9. Create a `StorageClass` using Azure Disk CSI

Define a `StorageClass` named `azure-premium-ssd` with the following specs:

```yaml
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: azure-premium-ssd
provisioner: disk.csi.azure.com
parameters:
  skuName: Premium_LRS
  kind: Managed
volumeBindingMode: WaitForFirstConsumer
allowVolumeExpansion: true
```

- **Provisioner**: `disk.csi.azure.com` – Azure CSI driver
- **skuName**: Use `Premium_LRS` for SSD-backed managed disks
- **volumeBindingMode**: `WaitForFirstConsumer` ensures the disk is provisioned in the same zone as the pod
- **allowVolumeExpansion**: Enables resizing volumes later

📚 Reference: [Azure Disk CSI Driver](https://learn.microsoft.com/en-us/azure/aks/azure-disk-csi)

10. Create a `PersistentVolumeClaim` using the Azure StorageClass

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: azure-storage-pvc
spec:
  accessModes:
    - ReadWriteOnce
  storageClassName: azure-premium-ssd
  resources:
    requests:
      storage: 5Gi
```

This will dynamically provision a 5Gi Azure-managed disk when a pod mounts the claim.

11. Deploy a pod using the dynamic claim

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: data-logger-azure
spec:
  containers:
    - name: logger
      image: busybox
      command: ["/bin/sh"]
      args:
        ["-c", "while true; do echo $(date) >> /data/log.txt; sleep 10; done"]
      volumeMounts:
        - name: azure-logs
          mountPath: /data
  volumes:
    - name: azure-logs
      persistentVolumeClaim:
        claimName: azure-storage-pvc
```

12. Apply your Azure-backed storage setup.

13. Validate Dynamic Provisioning in Azure

- Confirm PVC is **Bound**

- Confirm a dynamically created Azure Disk

- Optional: Check in the Azure Portal to view the provisioned disk under **Disks**

---

## Resources

- [Volumes](https://kubernetes.io/docs/concepts/storage/volumes/)
- [Persistent Volumes](https://kubernetes.io/docs/concepts/storage/persistent-volumes/)
- [Storage Classes](https://kubernetes.io/docs/concepts/storage/storage-classes/)
