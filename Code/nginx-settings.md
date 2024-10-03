When using the `kubectl create deployment nginx --image=nginx` command, you are quickly deploying an NGINX pod using the default NGINX configuration that comes with the `nginx` Docker image. However, this method doesn't allow you to directly provide a custom `nginx.conf` file.

To deploy NGINX with a custom configuration using `kubectl`, you will need to:

1. **Use a ConfigMap to inject the `nginx.conf` file** into the container.
2. **Mount the custom configuration into the NGINX pod** using a Kubernetes manifest file, rather than using the `kubectl create deployment` shortcut.

Here’s how you can do it by creating a deployment with a custom `nginx.conf` using `kubectl`:

### Steps to Inject Custom `nginx.conf` Using a ConfigMap

1. **Create a ConfigMap for the NGINX Configuration**

A ConfigMap can be used to store the `nginx.conf` file and inject it into your NGINX container.

First, create the custom `nginx.conf` file (example):

```nginx
# Custom nginx.conf
events { }

http {
    server {
        listen 80;
        server_name localhost;

        location / {
            root /usr/share/nginx/html;
            index index.html;
        }
    }
}
```

Create a ConfigMap using this `nginx.conf` file:

```bash
kubectl create configmap nginx-config --from-file=nginx.conf
```

This stores the `nginx.conf` file in a ConfigMap named `nginx-config`.

2. **Create a Deployment YAML with the Custom Configuration**

Now create a deployment manifest that uses the `nginx` image and mounts the custom `nginx.conf` file from the ConfigMap:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 1
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:latest
        ports:
        - containerPort: 80
        volumeMounts:
        - name: nginx-config-volume
          mountPath: /etc/nginx/nginx.conf
          subPath: nginx.conf
      volumes:
      - name: nginx-config-volume
        configMap:
          name: nginx-config
---
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  type: NodePort
  ports:
  - port: 80
    targetPort: 80
    nodePort: 30001
  selector:
    app: nginx
```

In this YAML file:
- The `volumeMounts` section mounts the ConfigMap (`nginx-config`) into the NGINX pod at `/etc/nginx/nginx.conf`.
- The `volumes` section specifies the ConfigMap as the source for the volume.
- The NGINX image uses the custom `nginx.conf` from the ConfigMap instead of the default one.

3. **Apply the YAML File to Create the Deployment and Service**

Save the YAML configuration as `nginx-deployment.yaml`, then apply it using `kubectl`:

```bash
kubectl apply -f nginx-deployment.yaml
```

This will create an NGINX deployment and service with the custom `nginx.conf` mounted from the ConfigMap.

4. **Access the Service**

Get the Minikube service URL with:

```bash
minikube service nginx-service --url
```

You can then access the NGINX service with the custom configuration.

### Summary

While the `kubectl create deployment` command is a quick way to deploy a basic NGINX server, it does not support custom configurations like `nginx.conf`. Instead, using a ConfigMap to store the custom `nginx.conf` and mounting it into the NGINX pod via a deployment manifest is the best approach. This allows you to customize NGINX configuration while leveraging Kubernetes features.