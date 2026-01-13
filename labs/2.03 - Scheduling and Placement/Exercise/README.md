# 🛰️ Lab 2.03 – Reinforced deployment protocol

## **Taints, Tolerations & Anti-Affinity**

## 🎯 Mission objectives

Secure the new **Star Destroyer node** by:

* Labeling it with Imperial allegiance: `alliance=Empire`
* Applying a **taint** to restrict access: `access=restricted:NoSchedule`
* Updating the **TIE Squadron Deployment** to:
  * Tolerate the Star Destroyer node’s taint
  * Use **pod anti-affinity** to prevent clustering on the same node
* Testing that a **Rebel craft** (e.g., X-wing) is denied access

---

## 🧭 Step-by-step: securing the station

### ⚙️ Phase I: Fortify the Star Destroyer Node

1. **Add an extra node pool**

Deploy a hardened node pool to serve as the Star Destroyer fleet platform:

```bash
export RESOURCE_GROUP="rg-aks-workshop"
export CLUSTER_NAME="aks-workshop-cluster"
export NODE_SIZE="Standard_E4ads_v6"
```

```bash
az aks nodepool add \
  --resource-group $RESOURCE_GROUP \
  --cluster-name $CLUSTER_NAME \
  --name destroyer \
  --node-count 3 \
  --node-vm-size $NODE_SIZE \
  --node-osdisk-type Ephemeral \
  --node-osdisk-size 64 \
  --mode User \
  --labels "alliance=Empire" \
  --node-taints "access=restricted:NoSchedule"
```

---

### ⚙️ Phase II: Configure Authorized TIE Fighter Deployment

2. **Modify your `squadron.yaml`**

Update the TIE squadron Deployment to:

* Add a **toleration** for `access=restricted:NoSchedule`
* Include **anti-affinity rules** to prevent TIE Fighters from clustering on a single node

---

### ⚙️ Phase III: Launch the Squadron

3. **Apply your Deployment**

```bash
kubectl apply -f squadron.yaml
```

4. **Verify Pod Placement**

```bash
kubectl get pods -o wide
```

✅ Confirm that pods:

* **Only land** on tainted Star Destroyer nodes
* Are **spread out** across different nodes via anti-affinity
* Have **not been scheduled** onto unapproved (untainted) nodes

---

### ⚙️ Phase IV: test Rebel infiltration

5. Taint the `aks-systempool` and `aks-userpool` nodes with `access=restricted:NoSchedule`
```bash
kubectl taint node aks-systempool-<<identifier>> access=restricted:NoSchedule
kubectl taint node aks-systempool-<<identifier>> access=restricted:NoSchedule
```

6. **Attempt to Deploy a Rebel Craft**

Create a pod with **no toleration**:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: xwing
spec:
  containers:
    - name: xwing
      image: nginx
      ports:
        - containerPort: 80
```

```bash
kubectl apply -f xwing.yaml
```

⛔ This pod should remain **unscheduled**, blocked by the taint on the Star Destroyer node.

```bash
kubectl describe pod xwing
```

Look for a message like:

> `0/3 nodes are available: 3 node(s) had taint {access=restricted: NoSchedule}, that the pod didn't tolerate.`

7. Untaint the `aks-systempool` and `aks-userpool` nodes
```bash
kubectl taint node aks-systempool-<<identifier>> access=restricted:NoSchedule-
kubectl taint node aks-systempool-<<identifier>> access=restricted:NoSchedule-
```

---

## 📚 Resources

* [Az CLI: Add Node Pool](https://learn.microsoft.com/en-us/cli/azure/aks/nodepool?view=azure-cli-latest#az-aks-nodepool-add)
* [Taints and Tolerations](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/)
* [Pod Affinity and Anti-Affinity](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#affinity-and-anti-affinity)
