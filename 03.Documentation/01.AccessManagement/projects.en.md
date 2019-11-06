---
title: Managing Access Using Projects
body_classes: title-center title-h1h2
published: true
---

Projects are the main entity used to control who has what permissions within iMKE.

<br/>

###New Projects
To create a new project go to [imke.cloud/projects](https://imke.cloud/projects) and select "Add Project" in the top-right corner, then enter the name you want and click "save".

<br/>

###Users
To add a new user to a project, when looking at any page within the project open the menu on the left and select "Members". Then in the members management screen click "Add Member" in the top-right corner. In the dialogue that appears enter the email for the user you want to add and select a group from the options listed below.

To Remove a user from a project navigate to the Members management page for the project, hover of the row for the user, and click the bin icon that appears on the right-hand side of the page.


### Groups
Users belong to one of three groups for each project they can access:

- Viewers: can examine information about clusters and node deployments, and can download kubeconfigs so that they can access the clusters they can view.
- Editors: can do everything Viewers can, as well as create, update, and delete clusters and node deployments.
- Owners: can do everything Editors can, as well as manage the members of the project. Make sure you trust the people you grant this access to as the are able to remove other owners from the project.

|Name|View Clusters|Edit Clusters|Edit Members|
|----|-------------|-------------|------------|
|Viewers|*| | |
|Editors|*|*| |
|Owners|*|*|*|