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