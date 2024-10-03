
@rifaterdemsahin ➜ /workspaces/minikubeoncodespaces (main) $ minikube addons enable ingress
❗  Executing "docker container inspect minikube --format={{.State.Status}}" took an unusually long time: 8.668267974s
💡  Restarting the docker service may improve performance.

❌  Exiting due to MK_ADDON_ENABLE_PAUSED: enabled failed: get state: unknown state "minikube": docker container inspect minikube --format=<no value>: exit status 1
stdout:


stderr:
Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running?


╭───────────────────────────────────────────────────────────────────────────────────────────╮
│                                                                                           │
│    😿  If the above advice does not help, please let us know:                             │
│    👉  https://github.com/kubernetes/minikube/issues/new/choose                           │
│                                                                                           │
│    Please run `minikube logs --file=logs.txt` and attach logs.txt to the GitHub issue.    │
│    Please also attach the following file to the GitHub issue:                             │
│    - /tmp/minikube_addons_20e9ef1a7cb2af32e95191af8ec0aa8b2b9f6d70_0.log                  │
│                                                                             