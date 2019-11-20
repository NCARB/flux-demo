# flux-get-started

We published a step-by-step run-through on how to use Flux and Helm Operator [over
here](https://github.com/fluxcd/flux/blob/master/docs/tutorials/get-started-helm.md).

## Manifests Validation

Github actions [jobs](./.github/workflow/):
* validate Kubernetes manifests with [kubeval](https://github.com/instrumenta/kubeval)

# Kubernetes

 * Developed in house by Google (Borg) and Open Sourced in 2014

 > Kubernetes is a portable, extensible, open-source platform for managing containerized workloads and services, that facilitates both declarative configuration and automation. It has a large, rapidly growing ecosystem. Kubernetes services, support, and tools are widely available.

 * "k8s"
<details>
 <summary>Growth and ecosystem</summary>

Kubernetes is now the second largest open source project in the world just behind linux.

Your company/organization manages containers with:

![Adaption rate](https://images.contentstack.io/v3/assets/blt300387d93dabf50e/blt23b893e26d9e5ab2/5bd0becf1a099f406f9837e7/download)

[From: CNCF Survey: CNCF Survey: Use of Cloud Native Technologies in Production Has Grown Over 200%](https://www.cncf.io/blog/2018/08/29/cncf-survey-use-of-cloud-native-technologies-in-production-has-grown-over-200-percent/#)

All major cloud vendors have rolled out managed k8s solutions (EKS, AKS, GKE...IBM, Digital Ocean)

</details>

<details>
<summary>Kubernetes Architecture 101</summary>

![](https://d33wubrfki0l68.cloudfront.net/817bfdd83a524fed7342e77a26df18c87266b8f4/3da7c/images/docs/components-of-kubernetes.png)

</details>


<details>
<summary>Kubernetes Objects and workloads</summary>

_source: https://cloud.netapp.com/blog/an-introduction-to-kubernetes_

# Cluster: 

The collective set of compute nodes and storage resources that form a Kubernetes environment. Each cluster has at least one master, which is responsible for overall management of the cluster, and a number of nodes on which containers will be scheduled to execute. Each node must have a container runtime installed, which is usually Docker.

# Pod: 

In the Kubernetes architecture, a set of containers may be deployed and scaled together. This is achieved by using pods, which are the minimum unit of deployment in a Kubernetes cluster, and allow more than one container to share the same resources, such as IP address, file systems, etc.

# Deployment: 

A deployment is used to control Kubernetes pod creation, updates, and scaling within the cluster, and is normally used for stateless applications. A stateless application does not depend on maintaining its own client session information, allowing any instance of the application to be equally capable of serving client requests.

# Services: 

Gateway to a set of running pods. When multiple, interchangeable pod replicas are active at the same time, clients need a simple way to find any active pod they can send requests to.

# Namespaces: 
Kubernetes supports multiple virtual clusters backed by the same physical cluster. These virtual clusters are called namespaces. This is ideal for sharing one cluster with multiple teams and environments (test vs prod)

Other Important things:

# Volume: 
A storage provisioned directly to a pod. Kubernetes supports a wide variety of volume types, including Amazon EBS, Azure Disk Storage, Google Persistent Disk, NFS, and many more. Volumes enable the containers within a pod to share information and are destroyed when their parent pod is deleted.

# Jobs and Cron Jobs: 
Jobs and Cron Jobs Kubernetes uses a workload called jobs to provide a more task-based workflow where the running containers are expected to exit successfully after some time once they have completed their work. Jobs are useful if you need to perform one-off or batch processing instead of running a continuous service. Cron Jobs are Jobs that run on a schedule

# ConfigMaps and Secrets: 
ConfigMaps can provide environment variables to a running container. Secrets can be manually applied to cluster or automatically pulled and synced with an external source (HashiCorp Vaut, AWS Secret Manager...)

</details>

<details>
<summary>Services vs Ingress</summary>

Service Types:

# ClusterIP:

the default. This allows a service to be accessible from within the cluster, but not from outside the cluster

# LoadBalancer:

![](https://matthewpalmer.net/kubernetes-app-developer/articles/loadbalancer.png)

This is typically heavily dependent on the cloud provider—GKE creates a Network Load Balancer with an IP address that you can use to access your service.

Every time you want to expose a service to the outside world, you have to create a new LoadBalancer and get an IP address.

![](https://matthewpalmer.net/kubernetes-app-developer/articles/ingress.png)

In contrast, an Ingress is a Kubernetes object that defines a set of rules (host, path etc) that route traffic to a service. This requires a "Ingress Controller" which defines a central LoadBalancer service and routes traffic accordingly. NGINX is the most popular

</details>


<details>
<summary>GitOps</summary>

>GitOps is a way to do Kubernetes cluster management and application delivery.  It works by using Git as a single source of truth for declarative infrastructure and applications. With Git at the center of your delivery pipelines, developers can make pull requests to accelerate and simplify application deployments and operations tasks to Kubernetes

#1. The entire system is described declaratively.

#2. The canonical desired system state is versioned in Git.

#3. Approved changes to the desired state are automatically applied to the system.

#4. Software agents ensure correctness and alert on divergence.

</details>

<details>
<summary>Flux</summary>

Open source kubernetes operator that syncs the state of the cluster with a git repo that declaritively describes the state of the cluster (source of truth). It can also pull new images from a docker registery based on a set of defined rules and automatically deploy new builds.

![](https://miro.medium.com/max/1021/1*kEMp1pP81Rzy2yXVjt4Gsg.png)

</details>

Notes on cluster setup for demo [here](./notes.md)

