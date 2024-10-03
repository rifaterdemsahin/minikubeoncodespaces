![alt text](/Resources/minikube.mdimg)

@rifaterdemsahin ➜ /workspaces/minikubeoncodespaces (main) $ kubectl config view
apiVersion: v1
clusters:
- cluster:
    certificate-authority: /home/codespace/.minikube/ca.crt
    extensions:
    - extension:
        last-update: Thu, 03 Oct 2024 18:38:12 UTC
        provider: minikube.sigs.k8s.io
        version: v1.34.0
      name: cluster_info
    server: https://192.168.49.2:8443
  name: minikube
contexts:
- context:
    cluster: minikube
    extensions:
    - extension:
        last-update: Thu, 03 Oct 2024 18:38:12 UTC
        provider: minikube.sigs.k8s.io
        version: v1.34.0
      name: context_info
    namespace: default
    user: minikube
  name: minikube
current-context: minikube
kind: Config
preferences: {}
users:
- name: minikube
  user:
    client-certificate: /home/codespace/.minikube/profiles/minikube/client.crt
    client-key: /home/codespace/.minikube/profiles/minikube/client.key
@rifaterdemsahin ➜ /workspaces/minikubeoncodespaces (main) $ 

///////////////////////////

@rifaterdemsahin ➜ /workspaces/minikubeoncodespaces (main) $ minikube status
minikube
type: Control Plane
host: Running
kubelet: Running
apiserver: Running
kubeconfig: Configured