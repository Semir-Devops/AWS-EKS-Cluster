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

 * API Server: Executes commands for you, this is done by UI or CLI (kubect).
 * Controller Manager: runs differrent controllers in your backend (for CRUD of your Nodes, pods etc.)
 * Scheduler: Schedules pod executions & queues API execute commands
 * etcd: A database for your Kubernetes cluster, contains information on your cluster (nodes/pods running etc.)

<ins><b>Master Node components:</b></ins>

 * Kubelet: This component of your WorkerNode is an agane that ensures your pods are healthy
 * Kube-proxy: This is where you maintain network rules/access to your nodes
 * Container-Runtime: This component executes run commands to your containers in your pods (Docker)
 * Pod: The smallest unit of your K8 cluster, this is where your containers live and are run
    * Container: The instance of your application which is run by docker

<hr/>

To create a Cluster we must store it into a network,

I have created a VPC in AWS using a CloudFormation template that was created by AWS (attached into my repo).<br/>When creating a VPC, feel free to use this document template or your own.

This allows us to run an EKS cluster within that network and allow access to it as we see fit

My VPC stack looks something like this:

![image](https://github.com/Semir-Devops/AWS-EKS-Cluster/assets/144611511/55f29362-9448-4061-b5e8-3239ac73a4fe)

<hr/>

The next thing to do is create IAM roles that allow your cluster to manage Master and Worker nodes.<br/>You must do this in order to run a Kubernetes cluster.

Go to IAM > Roles and create these roles with these permissions:

<b>eksClusterRole:</b>

![image](https://github.com/Semir-Devops/AWS-EKS-Cluster/assets/144611511/27653f53-01bc-410e-8aac-c1e1acd1e076)

<b>ec2WorkerNodeRole:</b>

![image](https://github.com/Semir-Devops/AWS-EKS-Cluster/assets/144611511/7b4f13f1-05a0-4964-9319-877952f13d35)

<hr/>

We are finally ready to create an EKS cluster. 

Head to EKS console in AWS and use the cluster Role as well as the VPC (with all subnets) you just created:

(A default VPC security group will be fine for this tutorial as well as Public & Private endpoint access to your cluster). 

![image](https://github.com/Semir-Devops/AWS-EKS-Cluster/assets/144611511/bb81ac96-3dde-4a87-9092-6042c98dc8d7)

<hr/>

The next step is to create an EC2 instance (t2.medium) that will act as your Master node.

Ensure you are able to SSH (in whatever mathod you choose) into it as we will be using kubectl to manage our cluster.



<hr/>

Once Creation is complete, navigate to the compute section of your cluster and create a Node Group.

I have attached a *Node1.json* file to the repo to show what a worker Node looks like.

When configuring:

 - Use WorkerNode role you created
 - all subnets of VPC created
 - Allow remote access to nodes
 - Use SSH keyPair (I have made sure the Master Node and worker nodes are using the same key pair, but this is up to you)
 - t3.medium instance type, minimum 20 GB space
 - Scaling configuration for Auto scaling of nodes (optional)

You should see your nodes after creating as such:

![image](https://github.com/Semir-Devops/AWS-EKS-Cluster/assets/144611511/013002b3-1c16-404c-9380-f0b6797ca432)

