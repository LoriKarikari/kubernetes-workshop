# 🧰 Lab 2.07.2 - Echoes in the Void: The Volume That Never Mounted

## 🎯 Scenario

You're deploying a PostgreSQL database using a Deployment and a PersistentVolumeClaim. The manifests are written, applied, and pods are scheduled. But the pod fails to start due to volume mounting issues. The PVC appears to be created—but something’s wrong.

---

## 🧭 Step-by-step

1. Apply the Manifests
2. Observe Pod Behavior
3. Troubleshoot the PVC and Volume Binding

---

## 🏁 Completion checklist

* [ ] Identified mismatch between PVC name in Deployment and actual PVC
* [ ] Verified the existence and correctness of the StorageClass
* [ ] Confirmed the pod starts and mounts volume successfully