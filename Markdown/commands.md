minikube start
minikube addons enable ingress
kubectl apply -f /workspaces/minikubeoncodespaces/Code/nginx-ingress.yaml
minikube ip