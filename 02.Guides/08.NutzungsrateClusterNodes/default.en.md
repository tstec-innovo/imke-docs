---
title: Cluster nodes usage rate
body_classes: title-center title-h1h2
published: false
---
When checking the cluster, we noticed an unusually high memory usage.
We see that one node is fully utilized while the other shows little load.
This often happens when a cluster with less than three nodes is upgraded at the nodes.
Here we explain how it comes to it.

## Finding Nodes Workload

First, let's see how many nodes are in the cluster  and what is the current load of cpu/memory.
![Step 1](get_top_node_1.png)

The command `kubectl top node` shows the current node utilization. In the example, there are two running nodes.

First the node is "cordoned", so that no new pods are scheduled to this node.

![Step 2](get_node_2.png)

Then the node is "drained",  so it is completely empty and the pods that used to run on the native node are distributed to all other nodes of the cluster.
With only two nodes, everything is placed on exactly the other node, then we will have a high loaded node.
![Step 3](top_node_3.png)

When the second node is back after the update, the pods will not be automatically distributed to both nodes. This leads to the initially observed imbalance.

## Here are some tips:
We recommend to use at least three nodes, because in that way loads could be better distributed during upgrades.
The web terminal has the tool `popeye`, which analyzes the cluster and makes suggestions for improvement based on best practices: https://docs.imke.cloud/en/guides/webterminal.
Upgrade the nodes to the latest version and follow the final step in the guide: https://docs.imke.cloud/en/guides/upgradingacluster.
