---
title: PodResourceManagement
body_classes: title-center title-h1h2
---

Pods have two main resource types that you need to know about: CPU and MEMORY. They are managed using requests and Limits within your resource definitons on either Pods, or Pod Templates (such as in a deployment). 

The CPU resource is measured in millicores. These are equivalent to 1/1000th of a CPU cores in your nodes. If you have a node with 2 physical cores that don't support hyperthreading then you will have 2000m available on that node. If you have 8 physical cores and they support hyperthreading then you will have 16000m available. In our openstack VMs you can use the specified Core count to work out CPU availability on that node.

Memory is measure in MB just like the RAM on your computer.

## How to use Resource Requests and Limits

You can assign limits to your pod using the 'resources' key in your manifests as shown here:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: cpu-demo-2
  namespace: cpu-example
spec:
  containers:
  - name: cpu-demo-ctr-2
    image: vish/stress
    resources:
      limits:
        cpu: "100"
        memory: "200Mi"
      requests:
        cpu: "100"
        memory: "200Mi"
```

If you don't understand the requirement for both requests and limits, or if you applications used a fixed amount of resources (common for JVM based systems) then it is recommended you set the requests and limits to the same values. More information on the difference can be found below.

Leaving these values unset can have unpredictable effects. If you don't specify a request it will be set to the default for your namespace, and if you don't set limits then your pods could potentially consume all of the resources available on the node.

If you have tried setting your requests and limits to the same value and things are working for you then you can stop reading here. In the sections below we will go into how the internal of the kubernetes scheduler and OS kernel resource manager work.

## How requests and limits work

### Requests

Requests are the primary resource used by the scheduler to work out how many pods, and which pods, can be scheduled on a given node. For requests the Kubernetes scheduler and OS resource manager work similarly but they do not interact at all. When a new node is created Kubernetes will evaluate how much CPU and Memory resources are available no that node and saves that value internally for tracking how much space there is still on the node. Once you have a node and you try to schedule a pod on it Kubernetes will make sure that the amount of resources available on that node are higher than what has been requseted by the pod. If Kubernetes detects that there is enough space on the node it will subtract the pod's requests from the node's available resources and schedule the pod to be executed on that node.

### Memory Limits

Memory limits are enforced by using the OOM manager in the host kernel. When the pod is created a [CGroup](https://en.wikipedia.org/wiki/Cgroups) is created to run it, and it's containers are started within that cgroup. 

### CPU Limits



In the OS CPU manager this translates to 