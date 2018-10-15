# Custom Solutions

[Reference Link](https://kubernetes.io/docs/setup/pick-right-solution/#custom-solutions)

If you do want to start from scratch, either because you have special requirements, or just because you want to understand what is underneath a Kubernetes cluster, try this guide.

## Designing and Preparing

### Learning

> 1. You should be familiar with using Kubernetes already, such as `kubectl` and concepts (pods, services, etc.).
>
> 2. You should  have `kubectl` installed on your desktop.

###Network

Kubernetes allocates an IP address to each pod. When creating a cluster, you need to allocate a block of IPs for Kubernetes to use as Pod IPs. The simplest approach is to allocate a different block of IPs to each node in the cluster as the node is added. A process in one pod should be able to communicate with another pod using the IP of the second pod. This connectivity can be accomplished in two ways:

* **Using an overlay network**
  * Provide encapsulation.
  * Encapsulation reduces performance.
* **Without an overlay network**
  * Configure the underlying network fabric (switches, routers, etc.) to be aware of pod IP addresses.
  * This does not require the encapsulation provided by an overlay, and so can achieve better performance.

There are various ways to implement one of the above options:

**1. Use a network plugin which is called by Kubernetes**

* Kubernetes supports the [CNI](https://github.com/containernetworking/cni) network plugin interface.

* There are a number of solutions which provide plugins for Kubernetes (listed alphabetically):

  > * [Calico](http://docs.projectcalico.org/)
  >
  > * [Flannel](https://github.com/coreos/flannel)
  >
  > * [Open vSwitch (OVS)](http://openvswitch.org/)
  >
  > * [Romana](http://romana.io/)
  >
  > * [Weave](http://weave.works/)
  >
  > * [More found here](https://kubernetes.io/docs/admin/networking#how-to-achieve-this/)

* You can also write your own.

**2. Compile support directly into Kubernetes**

* This can be done by implementing the “Routes” interface of a Cloud Provider module.
* The Google Compute Engine ([GCE](https://kubernetes.io/docs/setup/turnkey/gce/)) and [AWS](https://kubernetes.io/docs/setup/turnkey/aws/) guides use this approach.



**3. Configure the network external to Kubernetes**

* This can be done by manually running commands, or through a set of externally maintained scripts.
* You have to implement this yourself, but it can give you an extra degree of flexibility.

Kubernetes also allocates an IP to each [service](https://kubernetes.io/docs/concepts/services-networking/service/). However, service IPs do not necessarily need to be routable. The kube-proxy takes care of translating Service IPs to Pod IPs before traffic leaves the node.

Open any firewalls to allow access to the apiserver ports 80 and/or 443.

Enable ipv4 forwarding sysctl, `net.ipv4.ip_forward = 1`

Kubernetes enables the definition of fine-grained network policy between Pods using the [NetworkPolicy](https://kubernetes.io/docs/concepts/services-networking/network-policies/) resource. Not all networking providers support the Kubernetes NetworkPolicy API.

### Software Binaries

- etcd

- A container runner, one of:

  > * docker
  > * rkt

- Kubernetes

  > - kubelet
  > - kube-proxy
  > - kube-apiserver
  > - kube-controller-manager
  > - kube-scheduler

A Kubernetes binary release includes all the Kubernetes binaries as well as the supported release of etcd. Only using a binary release is covered in this guide.

### Downloading and Extracting Kubernetes Binaries

Download the [latest binary release](https://github.com/kubernetes/kubernetes/releases/latest) and unzip it.

 Server binary tarballs are no longer included in the Kubernetes final tarball, so you will need to locate and run `./kubernetes/cluster/get-kube-binaries.sh` to download the client and server binaries.

Then locate `./kubernetes/server/kubernetes-server-linux-amd64.tar.gz` and unzip *that*.



