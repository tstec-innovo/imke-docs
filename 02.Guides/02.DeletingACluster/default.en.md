---
title: Deleting a cluster
body_classes: title-center title-h1h2
published: false
---

It's quick and simple to delete Clusters in iMKE. The
only prerequisiste is that you need an existing Cluster
in an iMKE Project.


## Finding the Cluster

To delete a Cluster, we need to go into the Cluster's detail
view. For this we click on `first-system`:
![Step 1](delete_1.png)

We need to use the cluster name later. To copy it into the
paste buffer, we click on the name:
![Step 2](delete_2.png)

## Deleting the Cluster

Now we click `Delete`.
![Step 3](delete_3.png)

This opens a window where we need to enter the cluster name
to avoid sudden and unwanted deletions. Since we copied the name
into our paste buffer two steps previous, we can simply paste
it here.
![Step 4](delete_4.png)

Since we also want to free up the resources, we leave both check
boxes marked. That way, volumes and load balancers provided by
OpenStack will be removed as well.

## Summary

We learnt and achieved the following:
* How to delete a Cluster
* How to delete all Resources in OpenStack as well.

Congratulations! That's all you need to know to delete a Cluster in iMKE.
