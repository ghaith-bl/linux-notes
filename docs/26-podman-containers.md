# 26. Podman (Containers) — Bonus / RHCSA9+

## 26.1 Concept

- Daemonless, rootless-by-default container engine with a Docker-compatible CLI. Part of the RHCSA exam objectives on RHEL 9+.

## 26.2 Basic Commands

```bash
podman search <image>                 # Search for an image on configured registries
podman pull <image>                   # Download an image
podman images                         # List local images

podman run -d --name web -p 8080:80 nginx    # Run a container in the background
podman ps                             # List running containers
podman ps -a                          # List all containers (including stopped)

podman stop web
podman start web
podman rm web                         # Remove a stopped container
podman rmi <image>                    # Remove an image

podman logs web                       # View container logs
podman exec -it web /bin/bash         # Open a shell inside a running container
```

## 26.3 Running Containers as a systemd Service

```bash
podman generate systemd --name web --files
```
Generates a `.service` unit file so the container can be managed with `systemctl`.
