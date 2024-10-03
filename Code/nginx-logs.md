@rifaterdemsahin ➜ /workspaces/minikubeoncodespaces (main) $ kubectl get pods
NAME                     READY   STATUS    RESTARTS        AGE
nginx-676b6c5bbc-dvpsx   1/1     Running   2 (6m51s ago)   31m
@rifaterdemsahin ➜ /workspaces/minikubeoncodespaces (main) $ kubectl logs nginx-676b6c5bbc-dvpsx 
/docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
/docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
/docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
10-listen-on-ipv6-by-default.sh: info: Getting the checksum of /etc/nginx/conf.d/default.conf
10-listen-on-ipv6-by-default.sh: info: Enabled listen on IPv6 in /etc/nginx/conf.d/default.conf
/docker-entrypoint.sh: Sourcing /docker-entrypoint.d/15-local-resolvers.envsh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/30-tune-worker-processes.sh
/docker-entrypoint.sh: Configuration complete; ready for start up
2024/10/03 21:27:28 [notice] 1#1: using the "epoll" event method
2024/10/03 21:27:28 [notice] 1#1: nginx/1.27.2
2024/10/03 21:27:28 [notice] 1#1: built by gcc 12.2.0 (Debian 12.2.0-14) 
2024/10/03 21:27:28 [notice] 1#1: OS: Linux 6.5.0-1025-azure
2024/10/03 21:27:28 [notice] 1#1: getrlimit(RLIMIT_NOFILE): 1048576:1048576
2024/10/03 21:27:28 [notice] 1#1: start worker processes
2024/10/03 21:27:28 [notice] 1#1: start worker process 30
2024/10/03 21:27:28 [notice] 1#1: start worker process 31
@rifaterdemsahin ➜ /workspaces/minikubeoncodespaces (main) $ 