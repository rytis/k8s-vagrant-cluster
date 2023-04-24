# Introduction

Stand up K8s cluster on Vagrant managed VMs.

# Status

Multinode cluster:
- single control plane host, cluster initialised and CNI set up
- multiple worker nodes, joins cluster automatically

# Usage

- Clone the repository
- Run `vagrant up`

# Test

- `vagrant ssh k8s-c1`
- `KUBECONFIG=/etc/kubernetes/admin.conf kubectl get nodes` should show control plane and worker nodes in `Ready` state
