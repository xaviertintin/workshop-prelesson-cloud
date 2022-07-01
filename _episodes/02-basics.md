---
title: "Getting started with Argo and Kubectl"
teaching: 15
exercises: 15
questions:
- "How to setup a workflow engine to submit jobs?"
- "How to use Kubectl commands?"
- "What is kubectl?"
- "What is Argo workflows?"
- "What kind of services/resources will I need to instantiate in my cluster?"

objectives:
- "Understand how to run a simple workflows in a commercial cloud environment"
- "Lear what the kubectl command can do"
- "Appreciate the necessity for the Argo workflows tool (or similar)"
- "Lear how to set up different services/resources to get the most of your cluster"

keypoints:
- "kubectl is the ruler of GKE"
- "Argo is a very useful tool for running workflows and parallel jobs"
- "To be able to write, read and extract data, a few services/resources need to be set up on the GCP"
---

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


## The `kubectl` command

Just as `gcloud` is the *one command to rule them all* for the GCP, the `kubectl` command is the main tool for interacting with your K8s cluster. You will use it to do essentially anything in the cluster. [Here](https://kubernetes.io/docs/reference/kubectl/cheatsheet/) is the official *cheatsheet*, which is very useful but already very long.

Let's run a few examples.

* Get the status of the nodes in your cluster:

```
kubectl get nodes  
```

* Get the cluster info:

```
kubectl cluster-info  # Display addresses of the master and services

```

Let's list some kubernetes components:

* Check pods

```
kubectl get pod
```

* Check the services

```
kubectl get services
```

We don't have much going on.  Let's create some components.

* Inspect the `create` operation

```
kubectl create -h
```
Note there is no `pod` on the list, so in K8s you don't create pods but *deployments*.  These will create pods, which will run under the hood.

* Let's create an application, it does not matter which.  Let's go for `nginx`:

```
kubectl create deployment mynginx-depl --image=nginx
```

The `nginx` image will be pulled down from the Docker Hub.
This is the most minimalist way of creating a deployment.

* Check the deployments

```
kubectl get deployment
```

* Check pods

```
kubectl get pod
```

## Namespaces

Namespaces are a kind of reservations in your K8s cluster.  Let's create one for the Argo workflow we will user

```
kubectl create ns <NAMESPACE>
```

> ## Kubernetes namespaces
>
> The above commands as well as most of the following use a flag `-n argo`,
> which defines the namespace in which the resources are queried or created.
> [Namespaces](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/)
> separate resources in the cluster, effectively giving you multiple virtual
> clusters within a cluster.
>
> You can change the default namespace to `argo` as follows:
>
> ~~~
> kubectl config set-context --current --namespace=argo
> ~~~
> {: .bash}
>
{: .testimonial}

# Argo
Argo is a collection of open source tools that let us to extend the functions in Kubernetes. We can find some benefits from use argo.
- Cloud agnostic service
- Argo can execute on absolutely in all clusters in kubernetes.
- We can review the state of resources constantly.
- There is a large capacity of executing jobs at the same time and from different nodes.
- It’s possible correct debug errors.
We are going to explain 3 of the tools most important for working with argo.

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

## Argo as a workflow engine

While jobs can also be run manually, a workflow engine makes defining and
submitting jobs easier. In this tutorial, we use
[argo](https://argoproj.github.io/argo/quick-start/).
Install it into your working environment with the following commands
(all commands to be entered into the cloud shell):

While jobs can also be run manually, a workflow engine makes defining and submitting jobs easier. In this tutorial, we use [argo quick start](https://argoproj.github.io/argo-workflows/quick-start/) page to install it:

```
kubectl create ns argo
kubectl apply -n argo -f https://raw.githubusercontent.com/argoproj/argo-workflows/stable/manifests/quick-start-postgres.yaml
```

You can now check that argo is available with

```bash
argo version
```

We need to apply a small patch to the default argo config. Create a file called
`patch-workflow-controller-configmap.yaml`:

```yaml
data:
  artifactRepository: |
    archiveLogs: false
```

Apply:

```shell
kubectl patch configmap workflow-controller-configmap -n argo --patch "$(cat patch-workflow-controller-configmap.yaml)"
```

Run a simple test flow:

```
argo submit -n argo --watch https://raw.githubusercontent.com/argoproj/argo-workflows/master/examples/hello-world.yaml
argo list -n argo
argo get -n argo @latest
argo logs -n argo @latest
```

{% include links.md %}
