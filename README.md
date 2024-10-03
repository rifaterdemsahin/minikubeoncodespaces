# 🚀 Exposing NGINX on Minikube in Codespaces with Ingress

In this tutorial, I’ll walk you through the process of exposing an NGINX service on Minikube using an Ingress resource inside Codespaces. By the end, you’ll be able to access your NGINX service via a public DNS and domain name.

Let’s jump into it! 💡

## 1. Install NGINX Ingress Controller in Minikube

First, we need to enable the NGINX Ingress controller in Minikube. This handles traffic routing for your Ingress resources.

```bash
minikube start
minikube addons enable ingress
```

## 2. Create an NGINX Deployment 🖥️

Next, we’ll create an NGINX deployment to serve our content.

```bash
kubectl create deployment nginx --image=nginx
```

## 3. Expose NGINX as a ClusterIP Service

Expose the NGINX deployment internally via a ClusterIP service. This is necessary to route traffic through the Ingress.

```bash
kubectl expose deployment nginx --port=80 --target-port=80 --type=ClusterIP
```

## 4. Create an Ingress Resource 🌐

Now, let’s create an Ingress resource that routes traffic to the NGINX service. Save this YAML file as `nginx-ingress.yaml`:

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: nginx-ingress
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  rules:
  - host: nginx.local
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: nginx
            port:
              number: 80
```

Apply the Ingress configuration:

```bash
kubectl apply -f nginx-ingress.yaml
```

## 5. Configure DNS Resolution for Ingress Hostname 🗺️

To resolve the domain `nginx.local` to the IP of your Minikube instance, you’ll need to add it to your local `/etc/hosts` file.

```bash
minikube ip
```

Add this line to your `/etc/hosts` file (replacing `<minikube-ip>` with your Minikube IP):

```bash
<minikube-ip> nginx.local
```

Save the file to enable local DNS resolution.

## 6. Access NGINX via Ingress 🚀

Open your browser and go to:

```url
http://nginx.local
```

Alternatively, in Codespaces, forward port 80 using the Ports tab. Add a port forwarding rule, and you’ll get a generated URL.

## 7. Verify the Ingress Setup 🔍

Finally, confirm that your Ingress resource has been picked up by the NGINX Ingress controller:

```bash
kubectl get ingress
```

You should see `nginx-ingress` listed, indicating that the service is ready and accessible via the domain name.

---

💥 And that’s it! You’ve successfully set up NGINX with a LoadBalancer service using DNS and domain name configuration in Codespaces.

---

## 🔗 Connect with me:

- 💼 LinkedIn: [Rifat Erdem Sahin](https://www.linkedin.com/in/rifaterdemsahin/)
- 🐦 Twitter: [@rifaterdemsahin](https://x.com/rifaterdemsahin)
- 🎥 YouTube: [Rifat Erdem Sahin](https://www.youtube.com/@RifatErdemSahin)
- 💻 GitHub: [@rifaterdemsahin](https://github.com/rifaterdemsahin)

Need further help? Drop me a message! 👋
