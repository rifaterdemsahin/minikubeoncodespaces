@rifaterdemsahin ➜ /workspaces/minikubeoncodespaces (main) $ kubectl get pods
The connection to the server 192.168.49.2:8443 was refused - did you specify the right host or port?
@rifaterdemsahin ➜ /workspaces/minikubeoncodespaces (main) $ minikube start
😄  minikube v1.34.0 on Ubuntu 20.04 (docker/amd64)
✨  Using the docker driver based on existing profile
👍  Starting "minikube" primary control-plane node in "minikube" cluster
🚜  Pulling base image v0.0.45 ...
🏃  Updating the running docker "minikube" container ...
🐳  Preparing Kubernetes v1.31.0 on Docker 27.2.0 ...
🔎  Verifying Kubernetes components...
    ▪ Using image gcr.io/k8s-minikube/storage-provisioner:v5
🌟  Enabled addons: storage-provisioner, default-storageclass
🏄  Done! kubectl is now configured to use "minikube" cluster and "default" namespace by default
@rifaterdemsahin ➜ /workspaces/minikubeoncodespaces (main) $ kubectl get pods
NAME                     READY   STATUS    RESTARTS        AGE
nginx-676b6c5bbc-dvpsx   1/1     Running   2 (6m51s ago)   31m
@rifaterdemsahin ➜ /workspaces/minikubeoncodespaces (main) $ 