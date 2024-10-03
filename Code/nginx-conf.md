To deploy an NGINX application with a custom `nginx.conf` file to Minikube, you'll need to create a Kubernetes deployment that includes the custom NGINX configuration. Here's a step-by-step guide:

### 1. Prepare your NGINX Configuration (`nginx.conf`)
Create a custom `nginx.conf` file. Here’s an example of a basic configuration that listens on port 80:

```nginx
# nginx.conf
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

### 2. Create a Docker Image with the Custom NGINX Configuration

You need to build a Docker image that includes your custom `nginx.conf` file.

#### Create a `Dockerfile`:

```Dockerfile
# Use the official NGINX image as the base image
FROM nginx:alpine

# Copy your custom nginx.conf to the image
COPY nginx.conf /etc/nginx/nginx.conf

# Copy static website files or web app to the HTML root (optional)
COPY . /usr/share/nginx/html
```

In this `Dockerfile`:
- We use the official NGINX image (`nginx:alpine`).
- The custom `nginx.conf` is copied to the appropriate location in the container (`/etc/nginx/nginx.conf`).
- Optionally, you can copy any static files (e.g., `index.html`) to the `/usr/share/nginx/html` directory.

#### Build and Push the Docker Image

1. Build the Docker image (if you're using Minikube, ensure you're working with Minikube's Docker environment):

   ```bash
   eval $(minikube docker-env)
   docker build -t custom-nginx:latest .
   ```

2. Alternatively, if you're pushing the image to a registry (e.g., Docker Hub):

   ```bash
   docker build -t <your-dockerhub-username>/custom-nginx:latest .
   docker push <your-dockerhub-username>/custom-nginx:latest
   ```

### 3. Create Kubernetes Deployment and Service

Once the Docker image with the custom `nginx.conf` is ready, you can create a Kubernetes deployment and expose the service.

#### Create the Deployment YAML

Here is a basic `nginx-deployment.yaml` for Kubernetes, using your custom image:

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
        image: custom-nginx:latest   # Replace with your Docker image
        ports:
        - containerPort: 80
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

- In the `Deployment`, replace `custom-nginx:latest` with the name of your Docker image.
- The `Service` is of type `NodePort`, which exposes the NGINX service on a specific port (in this case, 30001) that you can access via Minikube.

#### Apply the Deployment and Service:

1. Deploy the YAML file to Minikube:

   ```bash
   kubectl apply -f nginx-deployment.yaml
   ```

2. Check if the deployment was created successfully:

   ```bash
   kubectl get pods
   ```

3. Check the service:

   ```bash
   kubectl get services
   ```

### 4. Access the NGINX Application in Minikube

1. You can use Minikube to get the service URL:

   ```bash
   minikube service nginx-service --url
   ```

2. Open the provided URL in your browser to access the NGINX server running with your custom configuration.

---

### Additional Notes:
- If you need HTTPS, configure SSL/TLS certificates in the `nginx.conf` file and mount them into the container.
- You can modify the `nginx.conf` to include specific routes, reverse proxies, or other advanced configurations depending on your use case.

This process allows you to deploy an NGINX server with custom configuration to a Minikube Kubernetes cluster.