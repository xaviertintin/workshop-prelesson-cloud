---
title: "Introduction"
teaching: 0
exercises: 0
questions:
- "What is Kubernetes?"
- "What is a Kubernetes cluster and why do I need one?"
objectives:
- "Learn the very basics of Kubernetes"
- "Learn a bit about the architecture of a Kubernetes cluster"
keypoints:
- "Kubernetes is an orchestrator of containers.  It is most useful when it is run in a cluster of computers"
- "Commercial K8s clusters are a good option for large computing needs."
- "We can run our containerized CMSSW jobs and subsequent analysis workflows in a K8s cluster."
---
## Introduction

Most of you have been working with Docker containers throughout this workshop.  As you know now, one could see these Docker containers like isolated machines that can run on a host machine in a very efficient way.  Your desktop or laptop could actually run several of these containers if enough resources are available.  For instance, you could think that one can maximize the hardware resources by running multiple CMSSW open data containers in one desktop.  Imagine, if you could run 10 CMSSW containers (each over a single root file) at the same time in a single physical machine, then it will take you 10 times less time to skim a full dataset.  




{% include links.md %}

