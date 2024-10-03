@rifaterdemsahin ➜ /workspaces/minikubeoncodespaces (main) $ kubectl create deployment nginx --image=nginx
error: failed to create deployment: Post "https://192.168.49.2:8443/apis/apps/v1/namespaces/default/deployments?fieldManager=kubectl-create&fieldValidation=Strict": dial tcp 192.168.49.2:8443: connect: connection refused
@rifaterdemsahin ➜ /workspaces/minikubeoncodespaces (main) $ 


The error you're encountering, `dial tcp 192.168.49.2:8443: connect: connection refused`, indicates that `kubectl` is unable to connect to the Minikube Kubernetes API server, possibly due to one of the following reasons:

### Troubleshooting Steps:

1. **Check if Minikube is running:**
   First, ensure that Minikube is running by using the following command:

   ```bash
   minikube status
   ```

   If Minikube is not running, start it:

   ```bash
   minikube start
   ```

2. **Ensure kubectl is using the Minikube context:**
   After starting Minikube, verify that `kubectl` is pointed at the correct Kubernetes context:

   ```bash
   kubectl config use-context minikube
   ```

   This sets the current context for `kubectl` to work with your Minikube cluster.

3. **Restart Minikube:**
   If Minikube is running but the connection is still refused, try restarting it to reset the cluster and connections:

   ```bash
   minikube stop
   minikube start
   ```

4. **Check Minikube IP:**
   Sometimes the Minikube IP might change, and `kubectl` might not be pointing to the right IP. Use the following command to check the Minikube IP:

   ```bash
   minikube ip
   ```

   Ensure that the IP matches with the one being used by `kubectl` in your context settings:

   ```bash
   kubectl config view
   ```

   If they don’t match, reconfigure the context or restart Minikube.

5. **Firewall and Network Issues:**
   If you’re using Codespaces, ensure that any local firewall settings are not blocking the connection between `kubectl` and Minikube. Additionally, check if your Codespaces networking is configured properly for Minikube.

After checking these steps, try running the deployment command again:

```bash
kubectl create deployment nginx --image=nginx
```

Let me know if the issue persists or if you need further help!