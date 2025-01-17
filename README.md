# Edgecase2024 Talos Workshop

# Export TALOSCONFIG
export TALOSCONFIG=./talosconfig

# Starting the Talos docker containers
docker compose up -d
## task 01

# Generate the Talos configuration 
talosctl gen config workshop https://172.20.0.100:6443 --kubernetes-version=1.29.7
## task 02

# Update Talos Config
talosctl config endpoint 172.20.0.100
talosctl config node 172.20.0.100
## task 03

# Create a patchfile (patch-docker.yaml)
machine:
  features:
    hostDNS:
      forwardKubeDNSToHost: true
## task 04

# Apply Talos Config
talosctl apply-config -f controlplane.yaml -n 172.20.0.100 --insecure -p @patch-docker.yaml
talosctl apply-config -f worker.yaml -n 172.20.0.150 --insecure -p @patch-docker.yaml
## task 05

# Dashboard (optional)
talosctl dashboard

# Bootstrap
talosctl bootstrap
talosctl health
## task 06

# Download kubeconfig
talosctl kubeconfig
## task 07

# Upgrade Talos CP & Worker
Change the version from 1.8.2 to 1.9.1 for both images (compose.yaml)
watch show-talos-version
docker compose up -d talos-cp
docker compose up -d talos-worker
## task 08

# Upgrade Kubernetes
talosctl upgrade-k8s --to=1.30.3
## task 09

# Run Workload
kubectl apply -f ./workload
## task 10