![alt text](/Resources/docker-output.png.png)

The error message "Client sent an HTTP request to an HTTPS server" indicates that your client (e.g., a browser or a tool like `curl`) is attempting to communicate with an NGINX server over plain HTTP, but the NGINX server is expecting HTTPS (encrypted communication using SSL/TLS).

This issue can occur when:

1. **The client is using HTTP** while the server is configured to use HTTPS (on port 443 by default).
2. The NGINX server is set up to only accept HTTPS connections, and you are accidentally trying to reach it via an HTTP request.

### To resolve the issue:

1. **Ensure you're using HTTPS**: If the NGINX server is configured to serve traffic over HTTPS, make sure the client is accessing the server using `https://` in the URL.
   - For example, use `https://your-domain.com` instead of `http://your-domain.com`.

2. **Check NGINX configuration**: Ensure that NGINX is properly configured to either:
   - **Redirect HTTP to HTTPS**: You can configure NGINX to automatically redirect HTTP traffic to HTTPS with the following configuration:

     ```nginx
     server {
         listen 80;
         server_name your-domain.com;
         return 301 https://$host$request_uri;
     }
     ```

   - **Serve both HTTP and HTTPS**: If you want NGINX to serve traffic on both protocols, ensure you have appropriate `server` blocks for both HTTP (port 80) and HTTPS (port 443).

3. **SSL/TLS certificate configuration**: If you're running HTTPS, ensure that SSL/TLS certificates are correctly set up and loaded in the NGINX configuration.

If you're still encountering the issue, feel free to share your NGINX configuration for a more detailed analysis.


/////////////

In Minikube, if you're running an NGINX server and encountering the "Client sent an HTTP request to an HTTPS server" error, here's how you can address it:

### Steps to resolve the issue:

1. **Ensure that NGINX is accessible over HTTP** if you don't need HTTPS, or configure the appropriate HTTPS handling if you want to serve traffic over HTTPS.

2. **Check NGINX configuration for SSL/TLS**: 
   If you're seeing this error, it's likely that NGINX is configured to serve HTTPS (on port 443), but you're trying to reach it using HTTP (on port 80). Here are a couple of ways to resolve this based on your needs:

#### Option 1: Serve only HTTP (if HTTPS is not required)
If you only want to serve traffic over HTTP and don't need HTTPS, modify your NGINX configuration to listen on port 80 without SSL. You can do this in your NGINX `deployment` or `nginx.conf`:

```nginx
server {
    listen 80;
    server_name your-minikube-service;
    
    location / {
        proxy_pass http://backend;
    }
}
```

This makes NGINX listen for plain HTTP requests.

#### Option 2: Redirect HTTP to HTTPS
If you want NGINX to accept HTTP requests and redirect them to HTTPS, add a redirect rule in your NGINX configuration. This ensures any HTTP request is automatically forwarded to HTTPS:

```nginx
server {
    listen 80;
    server_name your-minikube-service;

    # Redirect all HTTP requests to HTTPS
    return 301 https://$host$request_uri;
}
```

#### Option 3: Serve both HTTP and HTTPS
To serve both HTTP and HTTPS, ensure that NGINX is properly configured to handle requests on both ports. Here’s an example configuration:

```nginx
# HTTP server block
server {
    listen 80;
    server_name your-minikube-service;

    location / {
        proxy_pass http://backend;
    }
}

# HTTPS server block
server {
    listen 443 ssl;
    server_name your-minikube-service;

    ssl_certificate /etc/nginx/ssl/nginx.crt;
    ssl_certificate_key /etc/nginx/ssl/nginx.key;

    location / {
        proxy_pass https://backend;
    }
}
```

Make sure that the SSL certificates (`nginx.crt` and `nginx.key`) are correctly mounted in the pod and referenced in the NGINX configuration.

### Additional Minikube-Specific Steps:

1. **Expose the NGINX Service**:
   If you're running NGINX in a Kubernetes pod on Minikube, ensure you've exposed the service correctly to allow external access. For example, to expose an HTTP service running on port 80:

   ```bash
   kubectl expose deployment nginx --port=80 --target-port=80 --type=NodePort
   ```

   If you're serving HTTPS, you can expose it on port 443:

   ```bash
   kubectl expose deployment nginx --port=443 --target-port=443 --type=NodePort
   ```

2. **Access the NGINX service through Minikube**:
   You can get the URL to access the NGINX service by running:

   ```bash
   minikube service nginx --url
   ```

3. **Use HTTPS when required**:
   If the service is exposed on port 443 and configured for HTTPS, make sure you're using `https://` in your URL when accessing the service.

By following these steps, you can ensure that your NGINX service in Minikube is correctly handling HTTP and HTTPS traffic, avoiding the "Client sent an HTTP request to an HTTPS server" error.