# Introduction

Stand up K8s cluster on Vagrant managed VMs.

# Status

Multinode cluster:
- single control plane host, cluster initialised and CNI set up
- multiple worker nodes, need to be added maually

# Usage

- Clone the repository
- Run `vagrant up`
- Wait for all three hosts to come up
- On controller node (`k8s-c1`) run `kubeadm token create --print-join-command`
- Run the join command on worker nodes (`k8s-w1` and `k8s-w2`)

# Test

- `vagrant ssh k8s-c1`
- `KUBECONFIG=/etc/kubernetes/admin.conf kubectl get nodes` should show control plane and worker nodes in `Ready` state
