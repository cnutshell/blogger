# Setup

[Reference Link](https://kubernetes.io/docs/setup/)

## Conclusion

**Kubernetes can run on various platforms: from your laptop, to VMs on a cloud provider, to a rack of bare metal servers.** The effort required to set up a cluster varies from running a single command to crafting your own customized cluster.

If you just want to “**kick the tires**” on Kubernetes, use the [local Docker-based solutions](https://kubernetes.io/docs/setup/pick-right-solution/#local-machine-solutions).

When you are ready to scale up to more machines and higher availability, a [hosted solution](https://kubernetes.io/docs/setup/pick-right-solution/#hosted-solutions) is the easiest to create and maintain.

If you already have a way to configure hosting resources, use [kubeadm](https://kubernetes.io/docs/setup/independent/create-cluster-kubeadm/) to easily bring up a cluster with a single command per machine.

[Custom solutions](https://kubernetes.io/docs/setup/pick-right-solution/#custom-solutions) vary from step-by-step instructions to general advice for **setting up a Kubernetes cluster from scratch**.

## 1. [Local-machine Solutions](./Local-machine Solutions.md)

You can create and test Kubernetes clusters without worrying about consuming cloud resources and quotas. You should pick a local solution if you want to:

* **Try or start learning about Kubernetes**
* Develop and test clusters locally

## 2. Hosted Solutions

They manage and operate your clusters so you don’t have to. You should pick a hosted solution if you:

* Want a fully-managed solution
* **Want to focus on developing your apps or services**
* Don’t have dedicated site reliability engineering (SRE) team but want high availability
* Don’t have resources to host and monitor your clusters

## 3. Turnkey – Cloud Solutions

These solutions allow you to create Kubernetes clusters with only a few commands and are actively developed and have active community support. You should pick a turnkey **cloud** solution if you:

* Want more control over your clusters than the hosted solutions allow
* Want to take on more operations ownership

## 4. Turnkey – On-Premises Solutions

You should pick a **on-prem** turnkey cloud solution if you:

* Want to deploy clusters on your private cloud network
* **Have a dedicated SRE team**
* Have the resources to host and monitor your clusters

## 5. [Custom Solutions](./Custom Solutions.md)

Custom solutions give you the most freedom over your clusters but require the most expertise.
