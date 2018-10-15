# Local-machine Solutions

[Reference link](https://kubernetes.io/docs/setup/pick-right-solution/#local-machine-solutions)

## 1. Minikube

The recommended method for **creating a local, single-node Kubernetes cluster** for development and testing.

## 2. microk8s

Provides **a single command installation of the latest Kubernetes release** on a local machine for development and testing.

## 3. IBM Cloud Private-CE (Community Edition)

Use VirtualBox on your machine to deploy Kubernetes to one or more VMs.

## 4. IBM Cloud Private-CE (Community Edition) on Linux Containers

To create a seven node (1 Boot, 1 Master, 1 Management, 1 Proxy and 3 Workers) LXD cluster on Linux Host.

## 5. Kubeadm-dind

A multi-node (while minikube is single-node) Kubernetes cluster which only requires a docker daemon.

## 6. Ubuntu on LXD

Supports a nine-instance deployment on localhost.