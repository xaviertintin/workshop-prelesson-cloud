---
title: "Demo: Creating a cluster"
teaching: 5
exercises: 20
questions:
- "What are the basic concepts and jargon I need to know?"
- "Do do I manually create a K8s cluster on the GCP"
objectives:
- "Learn how to create a K8s cluster from scratch"
keypoints:
- "It takes just a few clicks to create you own K8s cluster"
---
## Introduction
In this demonstration we will show you the very basic way in which you can create a computer cluster (a Kubernetes cluster to be exact) in the cloud so you can do some data processing and analysis using those resources.  In the process we will make sure you learn about the jargon.  During the hands-on session of the workshop (cloud computing), a cluster similar to this one will be provided to you for the exercises.  

If needed you can watch a walkthrough [here](https://youtu.be/RPO6zR12iUc):

<iframe width="560" height="315" src="https://www.youtube.com/embed/RPO6zR12iUc" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

> ## Minikube
> 
> If you've opted to use [minikube](https://minikube.sigs.k8s.io/docs/start/), creating a kubernetes cluster is as easy as running:
> ```bash
> minikube start
> ```
> Feel free to skip to the [next episode](https://cms-opendata-workshop.github.io/workshop2022-lesson-introcloud/04-demo2/index.html).
{: .testimonial}


## Creating your own cluster on GKE
For the hands-on part of this lesson you will not have to create the cluster for yourself, it will be already done for you.  For pedagogical reasons, however, we will show an example of how to do it by hand. The settings below should be good and cheap enough for CMSSW-related workflows.

> Here you will find some [instructions on how to use preemptible machines](https://cloud.google.com/kubernetes-engine/docs/how-to/preemptible-vms#create_a_cluster_or_node_pool_with_preemptible_vms) in GKE.  Preemptible VMs offer similar functionality to Spot VMs, but only last up to 24 hours after creation, this might be taken into account if reducing costs is of your concern.
{: .testimonial}

* Get to the Console
* Create a new project or select one of your interest (if you already have one)
* Click on the Kubernetes engine/clusters section on the left side menu
![](../fig/SelectCluster.png)
* Select create cluster (standard)
![](../fig/SelectCreate.png)
* Select GKE Standard
![](../fig/SelectGKE.png)
* Give it a name
* Change the zone to ```europe-west1-b```
![](../fig/BasicClusterName.png)
* Many ways to configure the cluster, but let's try an efficient one with autoscaling
* Go to default pool
* Choose size: 1 node
* Autoscaling 0 to 4
  ![](../fig/ClusterDetails.png)
* Go to Nodes
* Choose a machine e2-standar-4
* Leave the rest as it is
* Hit create
![](../fig/MachineConfig.png)
* Creation will take while
While we wait, lets inspect the Cloud shell...
## Cloud shell
GCP provides an *access machine* so you can interact with their different services, including our newly created K8s cluster.  This machine (and the terminal) is not really part of the cluster. As was said, it is an entry point.  From here you could *connect* to your cluster.
## The `gcloud` command
The gcloud command-line interface is the primary CLI tool to create and manage Google Cloud resources. You can use this tool to perform many common platform tasks either from the command line or in scripts and other automations.
## Connect to your cluster
Once the cluster is ready (green check-mark should appear)
* Click on the connect button of your cluster:
![](../fig/Connection4.png)
* Execute that command in the cloud shell:
![](../fig/Commandline.png)
* You’ve connected to your shell, now press enter to link to your GKE cluster:
![](../fig/Load.png)
* Authorize Shell
![](../fig/SomeCredentials.png)
