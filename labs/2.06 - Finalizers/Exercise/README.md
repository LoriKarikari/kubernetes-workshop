# 🛰️ Lab 2.07 - Cleanup protocols – working with Finalizers


## 🎯 Mission objectives

- Add a **finalizer** to an existing `PersistentVolumeClaim` named `azure-datalog-claim`
- Attempt to delete the PVC and observe the block
- Confirm the PVC is stuck in **terminating**
- Remove the finalizer and force the deletion
- Do it all **declaratively** or using minimal imperative intervention

---

## 🧭 Step-by-step: using Finalizers

1. Inspect the `azure-datalog-claim` PVC

2. Edit the PVC to add a finalizer

3. Attempt to delete the PVC

4. Confirm that the PVC is **stuck in `Terminating`**

5. Remove the finalizer manually by editing the resource in a new terminal

```bash
kubectl patch pvc azure-datalog-claim -p '{"metadata":{"finalizers":[]}}' --type=merge
```

6. Confirm deletion

---

## 📚 Resources

- [Finalizers](https://kubernetes.io/docs/concepts/overview/working-with-objects/finalizers/)
