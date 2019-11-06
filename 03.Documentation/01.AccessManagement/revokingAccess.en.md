---
title: Revoking A User's Access
body_classes: title-center title-h1h2
published: true
---

Depending on how a user was access your systems this will be a little more or less involved. 

If a user had access to the iMKE dashboard then they have an OpenStack account which will need to be removed. Create a ticket on our [support page](https://support.innovo-cloude.de) and provide the email of the user to have our admins take care of that. If you need to remove them immediately and can't wait for that, then you can manually remove them from [projects](projects) by going to the members management page for the project, hovering over the row for the user, and clicking the bin icon that appears on the right-hand side.

You should then rotate the admin token for every cluster they had access to on the iMKE dashboard by going to each cluster's management page, selecting the 