---
title: "Demo: External IP"
teaching: 0
exercises: 10
questions:
- "What are the basic concepts and jargon I need to know?"
- "Do do I manually create a K8s cluster on the GCP"
objectives:
- "Learn a few words and concepts that will be used during this lesson"
- "Lear how to create a K8s cluster from scratch"
keypoints:
- "It takes just a few clicks to create you own K8s cluster"
---


## Cleaning workspace

Remember to delete your workflow again to avoid additional charges:
Run this until you get a message indicating there is no more workflows.

```shell
argo delete -n argo @latest
```

Delete namespace and delete all files

```shell
kubectl delete ns argo
rm *
rm -r *
```

Only delete your disk clame, if you used 
```shell
kubectl delete ns argo
rm *
rm -r *
```

Delete your disk
```shell
gcloud compute disks delete gce-nfs-disk-1 --zone=us-central1-c
```

