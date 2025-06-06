Great choice! ✅ Wiki.js is a powerful, modern, and lightweight wiki engine that runs well in Kubernetes and is much easier to manage than Discourse in this case. It uses a clean Node.js backend and supports multiple databases (like PostgreSQL or MySQL).

🧹 Step 1: Clean Up Old Resources
To completely remove your previous Discourse/Nextcloud setup:

bash
Copy
Edit
# Delete the namespace (removes everything inside)
kubectl delete namespace ask-canada

# Optional: Delete any leftover PVCs or PVs manually (if namespace delete doesn't do it)
kubectl get pvc --all-namespaces
kubectl delete pvc <pvc-name> -n <namespace>

kubectl get pv
kubectl delete pv <pv-name>

# Optional: Remove the local disk folder (only do this if you're sure!)
sudo rm -rf /mnt/data/*
🚀 Step 2: Deploy Wiki.js with NodePort + PostgreSQL (Standard YAML)
I'll provide you a Kubernetes setup using NodePort, no Helm needed, for easy customization.

🧾 Files You’ll Need:
Namespace

PersistentVolume & Claim

PostgreSQL Deployment

Wiki.js Deployment

NodePort Service

✅ Apply Everything in Order


bash
Copy
Edit
kubectl apply -f namespace.yaml
kubectl apply -f wiki-pv-pvc.yaml
kubectl apply -f postgres-deployment.yaml
kubectl apply -f wiki-deployment.yaml
kubectl apply -f wiki-service.yaml

🌐 Access Wiki.js
Once the pod is running, open your browser and visit:

cpp
Copy
Edit
http://<your-node-ip>:32080
You’ll see the Wiki.js setup screen — just follow the UI to finish configuration.



