# AWS-EKS-Cluster

This repository is committed to guiding you on how to create an EKS (Elastic Kubernetes Service) cluster on AWS.

Let's start by explaining what Kubernetes is, as EKS requires a good understanding of it.

Kubernetes in simplest terms, is a container orchestration tool that can automate the deployment, scaling, and management of containerized applications. Kubernetes does this by allowing to run Docker at exponentially higher availability as opposed to running docker containers regularly from a server, allowing you to write multiple applications in one cluster (consisting of Master-worker relationship nodes).

> [!NOTE]  
> Kubernetes is not a replacement to Docker, but rather an enhancement.

<ins>Some key features of Kubernetes include:</ins>
 - Automated Scheduling & Rollouts/Rollbacks
 - Storage Orchestration
 - Load Balancing

Below is an image of a basic Kubernetes cluster (which we will create):

![Kubernetes-cluster-architecture](https://github.com/Semir-Devops/AWS-EKS-Cluster/assets/144611511/4f834c22-e738-4929-864b-fc896091686e)

<ins><b>Master Node components:</b></ins>

 * API Server:
 * Controller Manager:
 * Scheduler:
 * etcd:

<ins><b>Master Node components:</b></ins>

 * Kubelet:
 * Kube-proxy:
 * Container-Runtime:
 * Pod:
    * Container:
