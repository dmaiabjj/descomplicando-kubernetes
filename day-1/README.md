# Descomplicando Kubernetes — Learning Repo

This repository contains hands-on materials for learning Kubernetes, starting with Day 1. It includes a local Kind cluster configuration and a simple Pod manifest you can apply to the cluster.

## Directory Structure

```
.
├── day-1/
│   ├── kind/
│   │   └── cluster.yaml   # Kind cluster: 1 control-plane, 2 workers
│   └── pod.yaml           # Example Pod running nginx on port 80
└── .git/                  # Git metadata
```

## Files Overview

- `day-1/kind/cluster.yaml`: Kind cluster configuration using API `kind.x-k8s.io/v1alpha4`.
  - Nodes: 1 control-plane, 2 workers.
- `day-1/pod.yaml`: Kubernetes Pod manifest named `ak8s`.
  - Image: `nginx`.
  - Port: containerPort 80.
  - Labels: `run=ak8s`.

## Quick Start

Prerequisites: Docker, Kind, and kubectl installed and available on your PATH.

1. Create a local Kind cluster:
   ```bash
   kind create cluster --name descomplicando-k8s --config day-1/kind/cluster.yaml
   ```
2. Verify the cluster:
   ```bash
   kubectl cluster-info
   kubectl get nodes -o wide
   ```
3. Deploy the example Pod:
   ```bash
   kubectl apply -f day-1/pod.yaml
   kubectl get pods -A
   ```
4. Optional: Port-forward to access nginx locally:
   ```bash
   kubectl port-forward pod/ak8s 8080:80
   # Open http://localhost:8080
   ```
5. Clean up the cluster when done:
   ```bash
   kind delete cluster --name descomplicando-k8s
   ```

## Notes

- The repo is organized by days (e.g., `day-1/`). Future days can add manifests, charts, and examples under their own folders.
- Manifests are kept minimal for clarity and can be extended with readiness probes, resource requests/limits, and services as you progress.

