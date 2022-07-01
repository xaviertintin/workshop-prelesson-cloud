---
title: "Introduction"
teaching: 10
exercises: 15
questions:
- "What is Kubernetes?"
- "What is Argo?"
objectives:
- "Learn the very basics of Kubernetes"
- "Learn the very basics of Argo"
keypoints:
- "First key point. Brief Answer to questions."
---
## What is Kubernetes?
Kubernetes is a container orchestration system open sourced by Google. Its main purpose is to schedule services to run on a cluster of computers while abstracting away the existence of the cluster from the services. Kubernetes is now maintained by the Cloud Native Computing Foundation, which is a part of the Linux Foundation. Kubernetes can flexibly handle replication, impose resource limits, and recover quickly from failures.

## Why you need Kubernetes?
Kubernetes provides you with a framework to run distributed systems resiliently. Kubernetes provides you with service discovery and load balancing, storage orchestration, automated rollouts and rollbacks, automatic bin packing, self-healing, secret and configuration management. 

## What is Kubernetes Cluster?
A Kubernetes cluster consists of "master" nodes and "worker" nodes. In short, master nodes share state to manage the cluster and schedule jobs to run on workers. It is considered best practice to run an odd number of masters.

## Kubernetes Components
When you deploy Kubernetes, you get a cluster. A Kubernetes cluster consists of a set of worker machines, called nodes. The worker nodes host the Pods that are the components of the application workload.

### Masters
Kubernetes masters share state via etcd, a distributed key-value store (KVS) implementing the Raft protocol. Do note that the state stored in etcd is scheduling state, service locations, and other cluster metadata; it does not keep state for the services running on the cluster.

### Workers
While master nodes are constantly sharing data, managing the control plane (routing inside the Kubernetes cluster), and scheduling services, workers primarily run pods.

## Nodes Components
### Pods 
In the Kubernetes world, pods are the smallest computing unit. A pod is made up of one or more containers. While pods are essential for understanding Kubernetes, when writing services we don't actually deal in pods but one further abstraction, deployments, which create pods for us|
### Kubelet 
The kubelet is the primary "node agent" that runs on each node.The kubelet takes a set of PodSpecs and ensures that the containers described in those PodSpecs are running and healthy. 
### Kube-Proxy 
It reflects the services defined in the cluster and manages the rules to load-balance requests to a service’s backend pods.

## Command line tool (kubectl)
Kubernetes provides a kubectl for communicating with a Kubernetes cluster's control plane, using the Kubernetes API.
Use the following syntax to run kubectl commands from your terminal window:
~~~
kubectl [command] [TYPE] [NAME] [flags]
~~~
where ```command ```, ```TYPE```, ```NAME```, and ```flags``` are:

```command:``` Specifies the operation that you want to perform on one or more resources, for example create, get, describe, delete.
<br />```TYPE:``` Specifies the resource type.
<br />```NAME:``` Specifies the name of the resource. 
<br /> ```flags:```Specifies optional flags. 
<br />
<br />For installation instructions, see [Installing kubectl](https://kubernetes.io/docs/tasks/tools/#kubectl); for a quick guide, see the [cheat sheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/).


# Argo
Argo is a collection of open source tools that let us to extend the functions in Kubernetes. We can find some benefits from use argo.
- Cloud agnostic service
- Argo can execute on absolutely in all clusters in kubernetes.
- We can review the state of resources constantly.
- There is a large capacity of executing jobs at the same time and from different nodes.
- It’s possible correct debug errors.
We are going to explain 3 of the tools most important for working with argo.
<p align="center">
  <img src="https://user-images.githubusercontent.com/70413460/176803763-43e3943f-0e55-47b0-8446-662d692dbb7a.png">
</p>

### 1. Argo workflow
- Is used to execute complex job orchestration, including serial and parallel execution where each stage is executed like a container.
- It is the most popular workflow execution engine for kubernetes.
- You can run thousands of workflows a day, each with thousands of concurrent tasks.
- Designed from the ground up for containers without the overhead and limitations of legacy VM and server-based environments. 

### 2. Argo Events
Argo events is an event-driven workflow automation framework for kubernetes. It allows you to trigger 10 different actions (such as the creation of Kubernetes objects, invoke workflows or serverless workloads) on over 20 different events (such as webhook, S3 drop, cron schedule, messaging queues - e.g. Kafka, GCP PubSub, SNS, SQS).
Features
Supports events from 20+ event sources and 10+ triggers.
Ability to customize business-level constraint logic for workflow automation.
Manage everything from simple, linear, real-time to complex, multi-source events.
CloudEvents compliant.

### 3. Argo CD
It is a controller within Kubernetes that continuously monitors running applications and compares their current status. It allows you to define a set of CRDs (Custom Resource Definitions) unlike others, it only implements repository monitoring by pulling. This means that in a certain time it reads each previously configured repository and applies all changes made in any modification.
##How to use ArgoCD?
When we want to implement GitOps, we will use some tools:
- minikube to have an environment with kubernetes on our machines.
- You will install Gitlab as a repository manager and continuous integration tool. We will configure two repositories: the first will simulate our application, and the second will simulate the configuration repository.
- Finally, install and configure ArgoCD on kubernetes for automatic deployment.


## Autoscaling
Kubernetes supports autoscaling to optimise your nodes’ resources as wll as adjust CPU and memory to meet your application’s real usage. When you need to save some money, you can scale down. Probably you want to pay for what you use, keep only with the resources when you need them
If you want to learn about pricing, ckeck the next link: [Google-cloud](https://cloud.google.com/compute/all-pricing)
