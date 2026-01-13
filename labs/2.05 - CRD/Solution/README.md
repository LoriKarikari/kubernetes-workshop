# 🛰️ Lab 2.09 - Communications relay – installing a Custom Resource Definition (CRD)

### **Imperial communications uplink – Gateway API deployment**

To strengthen control over star systems and patrol lanes, the Empire is upgrading its communications network. A new **Gateway API module** will be deployed to standardize traffic routing between sectors. But before starship traffic can be governed via this new interface, the core **Custom Resource Definitions (CRDs)** must be installed into the cluster.

As the systems engineer for Fleet Sector 9, your task is to install the **Gateway API CRDs** so that advanced routing policies and ingress gateways can be configured.

> _“Our data routes must be fortified. No unauthorized packets enter Imperial space.”_ – Admiral Ozzel

---

## 🎯 Mission objectives

- Install the official **Gateway API CRDs** into your Kubernetes cluster
- Verify that the CRDs are present
- Understand what new resource types were introduced

---

## 🧭 Step-by-step: installing an CRD

1. Install the Gateway API CRDs into your cluster (check the resources section for the latest version):

```bash
kubectl apply -f https://github.com/kubernetes-sigs/gateway-api/releases/download/v1.3.0/standard-install.yaml
```

1. Wait a few seconds, then list the installed CRDs

```bash
kubectl get crd
```

You should see CRDs such as:

- `gateways.gateway.networking.k8s.io`
- `httproutes.gateway.networking.k8s.io`
- `gatewayclasses.gateway.networking.k8s.io`

1. Inspect one of the installed CRDs to see its structure:

```bash
kubectl explain gateways.gateway.networking.k8s.io
```

---

## 📚 Resources

- [Introduction](https://gateway-api.sigs.k8s.io/)
- [Getting started with Gateway API](https://gateway-api.sigs.k8s.io/guides/)
- [Custom Resources](https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/)
