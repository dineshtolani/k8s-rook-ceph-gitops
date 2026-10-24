# Kubernetes Rook-Ceph GitOps

A hands-on Kubernetes infrastructure project managed through GitOps
using Argo CD and Helm.

## Infrastructure

- Kubernetes: kubeadm
- Operating system: Rocky Linux 9.8
- GitOps: Argo CD
- Load balancing: MetalLB
- Distributed storage: Rook-Ceph
- Container runtime: containerd
- Networking: Calico

## Goals

1. Manage infrastructure through GitOps.
2. Deploy MetalLB through reproducible configuration.
3. Install the Rook operator using Argo CD and Helm.
4. Deploy a Ceph cluster across three Kubernetes nodes.
5. Configure Ceph block storage and dynamic provisioning.
6. Validate persistent volumes and application workloads.
7. Practice Kubernetes, Rook, and Ceph upgrades.
8. Document troubleshooting, recovery, and upgrade procedures.

## Principles

- Pin software versions.
- Keep configuration in Git.
- Never commit credentials or secrets.
- Validate cluster health before upgrades.
- Test persistence and recovery.
- Document changes and lessons learned.
