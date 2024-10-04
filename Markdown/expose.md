kubectl expose deployment nginx --port=80 --target-port=80 --type=LoadBalancer
kubectl expose deployment nginx --port=80 --target-port=80 --type=ClusterIP

@rifaterdemsahin ➜ /workspaces/minikubeoncodespaces (main) $ kubectl delete svc nginx
service "nginx" deleted


@rifaterdemsahin ➜ /workspaces/minikubeoncodespaces (main) $  kubectl get svc
NAME         TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)   AGE
kubernetes   ClusterIP   10.96.0.1      <none>        443/TCP   3h20m
nginx        ClusterIP   10.97.65.118   <none>        80/TCP    8s
@rifaterdemsahin ➜ /workspaces/minikubeoncodespaces (main) $ curl http://10.97.65.118 