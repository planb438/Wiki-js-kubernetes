✅ Wiki.js is a powerful, modern, and lightweight wiki engine that runs well in Kubernetes and is much easier to manage than Discourse in this case. It uses a clean Node.js backend and supports multiple databases (like PostgreSQL or MySQL).

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

---

I now have Wiki.js install



🎉 Awesome — congrats on getting Wiki.js installed and running on your Kubernetes cluster! You're now ready to start building out your Ask Canada 🇨🇦 Q&A hub with a fast, modern, and extensible wiki system.

---

✅ What You Can Do Next:
Here are some useful next steps:
--
🛠️ 1. Secure Your Setup
Set up a domain (e.g. wiki.askcanada.ca) pointing to your node IP.

Use Ingress + Cert-Manager for automatic HTTPS with Let's Encrypt.

Restrict public editing or registration (if needed) under Admin > Users > Registration.
--
🗃️ 2. Customize Wiki.js for Ask Canada
🎨 Branding: Add your logo and adjust site name under Administration > Theme > General.

🧩 Extensions: Enable useful modules like Disqus, Google Analytics, Git sync, etc.

📚 Structure:

Create categories like Immigration, Education, Jobs, Taxes, etc.

Add FAQ-style pages under each, with content from your videos or scripts.

Embed YouTube videos with markdown like:

markdown
Copy
Edit
[![Watch on YouTube](https://img.youtube.com/vi/YOUR_VIDEO_ID/0.jpg)](https://www.youtube.com/watch?v=YOUR_VIDEO_ID)
--
🧠 3. Enable Community Q&A Features (Optional)
If you want users to collaborate more interactively:

Enable comments on articles.

Use an external service like Utterances (GitHub Issues-based) or Disqus.

In the long term, consider pairing with a Discourse or Flarum instance and linking discussions.
--
🚀 4. Enable Backups
Set up database and file backups for disaster recovery. Options:

pg_dump PostgreSQL manually or via cronjob pod

Mount a separate PVC or S3 bucket (Wiki.js can sync content to Git as well)

💡 Optional: Git-based Content Sync
You can connect your content to a GitHub repo:

Go to Administration > Git

Wiki.js will push/pull pages to/from a repo, so you always have version control.

Would you like help with:

Adding Ingress + TLS

Enabling GitHub content sync

Automating backups

Connecting it to a custom domain

Creating a contributor guide

Let me know where you’d like to go next.
