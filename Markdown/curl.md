@rifaterdemsahin ➜ /workspaces/minikubeoncodespaces (main) $ minikube ip
192.168.49.2
@rifaterdemsahin ➜ /workspaces/minikubeoncodespaces (main) $ curl 192.168.49.2
curl: (7) Failed to connect to 192.168.49.2 port 80: Connection refused
@rifaterdemsahin ➜ /workspaces/minikubeoncodespaces (main) $ curl https://192.168.49.2

@rifaterdemsahin ➜ /workspaces/minikubeoncodespaces (main) $ curl https://192.168.49.2
curl: (7) Failed to connect to 192.168.49.2 port 443: Connection refused
@rifaterdemsahin ➜ /workspaces/minikubeoncodespaces (main) $ kubectl get svc
NAME         TYPE           CLUSTER-IP       EXTERNAL-IP   PORT(S)        AGE
kubernetes   ClusterIP      10.96.0.1        <none>        443/TCP        3h15m
nginx        LoadBalancer   10.106.120.168   <pending>     80:30810/TCP   55m
@rifaterdemsahin ➜ /workspaces/minikubeoncodespaces (main) $ curl https://10.106.120.168 
^C
@rifaterdemsahin ➜ /workspaces/minikubeoncodespaces (main) $ curl https://10.106.120.168:30180
^C
@rifaterdemsahin ➜ /workspaces/minikubeoncodespaces (main) $ curl http://10.106.120.168:30180
^[[A^C
@rifaterdemsahin ➜ /workspaces/minikubeoncodespaces (main) $ curl https://10.96.0.1  