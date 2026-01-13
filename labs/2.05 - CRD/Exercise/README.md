# 🛰️ Lab 2.09 - Communications relay – installing a Custom Resource Definition (CRD)


## 🎯 Mission objectives

- Install the official **Gateway API CRDs** into your Kubernetes cluster
- Verify that the CRDs are present
- Understand what new resource types were introduced

---

## 🧭 Step-by-step: installing an CRD

1. Install the Gateway API CRDs into your cluster (check the resources section for the latest version):

2. Wait a few seconds, then list the installed CRDs

You should see CRDs such as:

- `gateways.gateway.networking.k8s.io`
- `httproutes.gateway.networking.k8s.io`
- `gatewayclasses.gateway.networking.k8s.io`

3. Inspect one of the installed CRDs to see its structure:

```bash
kubectl explain gateways.gateway.networking.k8s.io
```

---

## 📚 Resources

- [Introduction](https://gateway-api.sigs.k8s.io/)
- [Getting started with Gateway API](https://gateway-api.sigs.k8s.io/guides/)
- [Custom Resources](https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/)
