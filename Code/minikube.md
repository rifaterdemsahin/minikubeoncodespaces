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

////////////////////////

@rifaterdemsahin ➜ /workspaces/minikubeoncodespaces (main) $ kubectl get pods
NAME                     READY   STATUS    RESTARTS      AGE
nginx-676b6c5bbc-dvpsx   1/1     Running   1 (21m ago)   21m
@rifaterdemsahin ➜ /workspaces/minikubeoncodespaces (main) $ 


////////////////////

@rifaterdemsahin ➜ /workspaces/minikubeoncodespaces (main) $ kubectl get events --watch
LAST SEEN   TYPE     REASON                    OBJECT                        MESSAGE
174m        Normal   Starting                  node/minikube                 Starting kubelet.
174m        Normal   NodeHasSufficientMemory   node/minikube                 Node minikube status is now: NodeHasSufficientMemory
174m        Normal   NodeHasNoDiskPressure     node/minikube                 Node minikube status is now: NodeHasNoDiskPressure
174m        Normal   NodeHasSufficientPID      node/minikube                 Node minikube status is now: NodeHasSufficientPID
174m        Normal   NodeAllocatableEnforced   node/minikube                 Updated Node Allocatable limit across pods
174m        Normal   Starting                  node/minikube                 Starting kubelet.
174m        Normal   NodeAllocatableEnforced   node/minikube                 Updated Node Allocatable limit across pods
174m        Normal   NodeHasSufficientMemory   node/minikube                 Node minikube status is now: NodeHasSufficientMemory
174m        Normal   NodeHasNoDiskPressure     node/minikube                 Node minikube status is now: NodeHasNoDiskPressure
174m        Normal   NodeHasSufficientPID      node/minikube                 Node minikube status is now: NodeHasSufficientPID
174m        Normal   RegisteredNode            node/minikube                 Node minikube event: Registered Node minikube in Controller
174m        Normal   Starting                  node/minikube                 
36m         Normal   Starting                  node/minikube                 Starting kubelet.
36m         Normal   NodeHasSufficientMemory   node/minikube                 Node minikube status is now: NodeHasSufficientMemory
36m         Normal   NodeHasNoDiskPressure     node/minikube                 Node minikube status is now: NodeHasNoDiskPressure
36m         Normal   NodeHasSufficientPID      node/minikube                 Node minikube status is now: NodeHasSufficientPID
36m         Normal   NodeAllocatableEnforced   node/minikube                 Updated Node Allocatable limit across pods
36m         Normal   RegisteredNode            node/minikube                 Node minikube event: Registered Node minikube in Controller
36m         Normal   Starting                  node/minikube                 
34m         Normal   Starting                  node/minikube                 Starting kubelet.
34m         Normal   NodeHasSufficientMemory   node/minikube                 Node minikube status is now: NodeHasSufficientMemory
34m         Normal   NodeHasNoDiskPressure     node/minikube                 Node minikube status is now: NodeHasNoDiskPressure
34m         Normal   NodeHasSufficientPID      node/minikube                 Node minikube status is now: NodeHasSufficientPID
34m         Normal   NodeAllocatableEnforced   node/minikube                 Updated Node Allocatable limit across pods
33m         Normal   Starting                  node/minikube                 
33m         Normal   RegisteredNode            node/minikube                 Node minikube event: Registered Node minikube in Controller
5m8s        Normal   Starting                  node/minikube                 Starting kubelet.
5m8s        Normal   NodeHasSufficientMemory   node/minikube                 Node minikube status is now: NodeHasSufficientMemory
5m8s        Normal   NodeHasNoDiskPressure     node/minikube                 Node minikube status is now: NodeHasNoDiskPressure
5m8s        Normal   NodeHasSufficientPID      node/minikube                 Node minikube status is now: NodeHasSufficientPID
5m8s        Normal   NodeAllocatableEnforced   node/minikube                 Updated Node Allocatable limit across pods
5m1s        Normal   Starting                  node/minikube                 
5m          Normal   RegisteredNode            node/minikube                 Node minikube event: Registered Node minikube in Controller
2m27s       Normal   Starting                  node/minikube                 Starting kubelet.
2m26s       Normal   NodeHasSufficientMemory   node/minikube                 Node minikube status is now: NodeHasSufficientMemory
2m26s       Normal   NodeHasNoDiskPressure     node/minikube                 Node minikube status is now: NodeHasNoDiskPressure
2m27s       Normal   NodeHasSufficientPID      node/minikube                 Node minikube status is now: NodeHasSufficientPID
2m27s       Normal   NodeAllocatableEnforced   node/minikube                 Updated Node Allocatable limit across pods
2m19s       Normal   Starting                  node/minikube                 
2m18s       Normal   RegisteredNode            node/minikube                 Node minikube event: Registered Node minikube in Controller
36m         Normal   Scheduled                 pod/nginx-676b6c5bbc-dvpsx    Successfully assigned default/nginx-676b6c5bbc-dvpsx to minikube
36m         Normal   Pulling                   pod/nginx-676b6c5bbc-dvpsx    Pulling image "nginx"
36m         Normal   Pulled                    pod/nginx-676b6c5bbc-dvpsx    Successfully pulled image "nginx" in 9.205s (9.205s including waiting). Image size: 191645082 bytes.
36m         Normal   Created                   pod/nginx-676b6c5bbc-dvpsx    Created container nginx
36m         Normal   Started                   pod/nginx-676b6c5bbc-dvpsx    Started container nginx
33m         Normal   SandboxChanged            pod/nginx-676b6c5bbc-dvpsx    Pod sandbox changed, it will be killed and re-created.
33m         Normal   Pulling                   pod/nginx-676b6c5bbc-dvpsx    Pulling image "nginx"
33m         Normal   Pulled                    pod/nginx-676b6c5bbc-dvpsx    Successfully pulled image "nginx" in 981ms (981ms including waiting). Image size: 191645082 bytes.
33m         Normal   Created                   pod/nginx-676b6c5bbc-dvpsx    Created container nginx
33m         Normal   Started                   pod/nginx-676b6c5bbc-dvpsx    Started container nginx
5m3s        Normal   SandboxChanged            pod/nginx-676b6c5bbc-dvpsx    Pod sandbox changed, it will be killed and re-created.
5m1s        Normal   Pulling                   pod/nginx-676b6c5bbc-dvpsx    Pulling image "nginx"
5m1s        Normal   Pulled                    pod/nginx-676b6c5bbc-dvpsx    Successfully pulled image "nginx" in 983ms (983ms including waiting). Image size: 191645082 bytes.
5m          Normal   Created                   pod/nginx-676b6c5bbc-dvpsx    Created container nginx
5m          Normal   Started                   pod/nginx-676b6c5bbc-dvpsx    Started container nginx
2m21s       Normal   SandboxChanged            pod/nginx-676b6c5bbc-dvpsx    Pod sandbox changed, it will be killed and re-created.
2m20s       Normal   Pulling                   pod/nginx-676b6c5bbc-dvpsx    Pulling image "nginx"
2m19s       Normal   Pulled                    pod/nginx-676b6c5bbc-dvpsx    Successfully pulled image "nginx" in 965ms (965ms including waiting). Image size: 191645082 bytes.
2m19s       Normal   Created                   pod/nginx-676b6c5bbc-dvpsx    Created container nginx
2m18s       Normal   Started                   pod/nginx-676b6c5bbc-dvpsx    Started container nginx
36m         Normal   SuccessfulCreate          replicaset/nginx-676b6c5bbc   Created pod: nginx-676b6c5bbc-dvpsx
36m         Normal   ScalingReplicaSet         deployment/nginx              Scaled up replica set nginx-676b6c5bbc to 1
