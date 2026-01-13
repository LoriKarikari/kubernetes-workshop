# 🛰️ Lab 2.04 - Squadron clearance – Service Accounts in action

## 🎯 Mission objectives

You will:

1. Create a **ServiceAccount** for the squadron using a **declarative manifest**.
2. Modify the **`squadron` Deployment manifest** to use this ServiceAccount.
3. Apply the changes and **verify** that the pods are using the correct identity.

All tasks must be completed as **declaratively as possible**—use manifests, not imperative commands.

---

## 🧭 Step-by-step: assigning identity to Imperial units

1.  Create the ServiceAccount Manifest

Create a YAML manifest file for the ServiceAccount `sa-squadron.yaml` with the following specification:

* namespace: default
* name: sa-squadron

---

2.  Update the Deployment Manifest

Update your existing `squadron.yaml` deployment to include the `serviceAccountName` field

---

3.  Verify Pod Identity

Confirm that the squadron pods are using the correct service account

You should see all pods using `sa-squadron`.

---

## 📚 Resources

- [Service Accounts](https://kubernetes.io/docs/concepts/security/service-accounts/)
- [Configure Service Accounts for Pods](https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/)
