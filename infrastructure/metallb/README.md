# MetalLB

## Purpose

MetalLB provides external IP addresses for Kubernetes
LoadBalancer services in this VMware-based Kubernetes lab.

## Environment

- Kubernetes: v1.34.12
- Operating system: Rocky Linux 9.8
- Container runtime: containerd
- CNI: Calico
- Node network: 192.168.170.0/24
- Advertisement mode: Layer 2
- Helm chart: metallb
- Chart version: 0.16.1

## Architecture

MetalLB assigns IP addresses to Kubernetes LoadBalancer
services and advertises them on the network.

The configuration consists of:

- IPAddressPool: defines available service IP addresses.
- L2Advertisement: configures Layer 2 announcements.

## Address pool

192.168.170.220-192.168.170.230

These addresses must be reserved for MetalLB and excluded
from DHCP allocation.

## Argo CD exposure

The Argo CD server uses a Kubernetes LoadBalancer service.

Current external IP:

192.168.170.220

## GitOps design

Argo CD manages the MetalLB Helm chart and configuration
through separate Applications.

## Validation

Check the Helm release:

    helm list -n metallb-system

Check MetalLB pods:

    kubectl get pods -n metallb-system -o wide

Check the address pool:

    kubectl get ipaddresspools.metallb.io -n metallb-system

Check Layer 2 advertisements:

    kubectl get l2advertisements.metallb.io -n metallb-system

Check LoadBalancer services:

    kubectl get svc -A | grep LoadBalancer

## Troubleshooting

Inspect workloads:

    kubectl get deployments,daemonsets -n metallb-system

Inspect recent events:

    kubectl get events -n metallb-system \
      --sort-by=.lastTimestamp

Inspect controller logs:

    kubectl logs -n metallb-system \
      deployment/metallb-controller

Inspect speaker logs:

    kubectl logs -n metallb-system \
      daemonset/metallb-speaker

## Official documentation

- https://metallb.io/installation/
- https://metallb.io/configuration/
- https://metallb.io/concepts/layer2/
- https://metallb.io/troubleshooting/
