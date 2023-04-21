# Introduction

Stand up K8s cluster on Vagrant managed VMs.

# Status

Only single node configuration (control plane) is implemented.

# Usage

- Clone the repository
- Run `vagrant up`

# Test

- `vagrant ssh`
- `KUBECONFIG=/etc/kubernetes/admin.conf kubectl get nodes` should show control plane node in `Ready` state
