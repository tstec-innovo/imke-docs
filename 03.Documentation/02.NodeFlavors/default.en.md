---
title: Choosing Node Flavors / Sizes
body_classes: title-center title-h1h2
published: true
---

During the setup of new nodes in a cluster you can select a respective "flavor" for that node.

<img src="flavor-select.png" width="600" height="65"/>
	
Flavors determine the amount of processing cores ("CPUs"), Memory ("GB RAM") and disk space ("GB Disk") of the respective node.

<img src="flavors.png" width="600" height="500"/>

A good practice for choosing the right flavor for your project is cycling through the following steps:
1. Start by selecting a small flavor.
2. Evaluate the performance of the desired use case.
3. Pick a larger flavor in case of any issues.
 
## Flavors ändern

Changing the flavor of a node at any point in time is as easy as following these steps:

1. Navigate to the desired cluster.

    <img src="clusters.png" width="1500" height="300"/>

2. Click the Edit-Icon on the node for which you would like to select another flavor. The Icon becomes visible when hovering over the node with your mouse.

    <img src="node-selection.png" width="1500" height="700"/>

3. Select the desired flavor and click the "Edit Node Deployment"-button when you're finished.

    <img src="edit-node.png" width="600" height="700"/>

Soon after performing these steps, a confirmation message pops up and your node flavor has been changed successfully.