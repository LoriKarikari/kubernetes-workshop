# 🧰 Lab 3.09.5 - The Phantom Startup: Echoes from the Init Bay

## 🎯 Scenario

You’re deploying a multi-container pod with init containers designed to prepare a database before the main application starts. The pod also includes a sidecar container for log shipping. After deployment, the application fails to start properly, and some containers don’t behave as expected.

---

## 🧭 Step-by-step

1. Apply all manifests under the scenario directory
```bash
kubectl apply -f configmap.yaml
kubectl apply -f database.yaml
kubectl apply -f deployment.yaml
```

2. Observe pod status and container logs
3. Investigate init container and sidecar behaviors
4. Troubleshoot volume mounts, file dependencies, and container readiness

---

## 🏁 Completion checklist

* [ ] Verified that init containers complete successfully
* [ ] Checked the shared volume for expected readiness files
* [ ] Confirmed volume mount names are consistent across containers
* [ ] Validated proper sequencing of database initialization and pod startup
* [ ] Examined script permissions and execution within init containers

---

## 📚 Resources

- [Mysql CLI Commands](https://dev.mysql.com/doc/refman/5.7/en/command-line-options.html)