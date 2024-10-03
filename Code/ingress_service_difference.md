These Kubernetes YAML configurations define different types of Kubernetes resources that work together to manage and expose the `nginx` application in a cluster. Here's the difference between them:

1. **Service (LoadBalancer Type)**:
   ```yaml
   apiVersion: v1
   kind: Service
   metadata:
     name: nginx-loadbalancer
   spec:
     type: LoadBalancer
     selector:
       app: nginx
     ports:
       - protocol: TCP
         port: 80
         targetPort: 80
   ```
   - **Purpose**: Defines a Service of type `LoadBalancer`. A Service is used to expose the `nginx` Pods internally or externally to the internet.
   - **Type**: `LoadBalancer` type Service exposes the `nginx` Pods to an external IP, allowing external traffic to access the application on port 80.
   - **Selector**: `selector: app: nginx` ensures that this Service will route traffic to Pods with the `app: nginx` label.
   - **Ports**: The Service listens on port 80, forwarding traffic to the target port (also 80) on the selected Pods.

2. **Deployment**:
   ```yaml
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: nginx-deployment
   spec:
     replicas: 2
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
   ```
   - **Purpose**: A Deployment manages the lifecycle of the `nginx` Pods.
   - **Replicas**: It defines 2 replicas (2 instances) of the `nginx` Pods, ensuring high availability.
   - **Pod Template**: The `template` section defines the Pod specification, where the container image (`nginx:latest`) and container port (80) are specified.
   - **Selector**: The `selector` ensures that the Deployment manages Pods labeled with `app: nginx`.

3. **Ingress**:
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
   - **Purpose**: An Ingress manages external access to the services inside the cluster. It defines routing rules for incoming HTTP/HTTPS requests.
   - **Host**: It defines a rule for the host `nginx.local`, routing traffic to the specified service.
   - **Backend**: The Ingress forwards traffic to the Service named `nginx` (this would need to match the Service name in the cluster) on port 80.
   - **Annotations**: `nginx.ingress.kubernetes.io/rewrite-target: /` ensures that requests to any path are forwarded to the root of the service (i.e., `/`).

### Key Differences:
- **Service**: Exposes Pods, routing traffic to them (in this case externally with LoadBalancer).
- **Deployment**: Manages the lifecycle of Pods, ensuring availability and scaling them (2 replicas in this case).
- **Ingress**: Provides routing rules for external HTTP/HTTPS traffic, directing requests to the Service based on rules and hosts.

Together, these resources form a Kubernetes-based system where the Deployment runs `nginx`, the Service exposes it to the outside world, and the Ingress manages routing rules.
