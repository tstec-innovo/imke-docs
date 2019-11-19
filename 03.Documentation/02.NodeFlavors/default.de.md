---
title: Node-Flavors (Leistung) konfigurieren
body_classes: title-center title-h1h2
published: true
---

Während der Erstellung von Nodes in einem Cluster kann man sich zwischen diversen sogenannten "Flavors" entscheiden.

<img src="flavor-select.png" width="600" height="65"/>
	
Flavors bestimmen die Anzahl an Prozessorkernen ("CPUs") und Speicher ("GB RAM"), sowie die Festplattengröße ("GB Disk") der entsprechenden Node.

<img src="flavors.png" width="600" height="500"/>

Hilfreich bei der Auswahl des richtigen Flavors sind die folgenden, wiederholbaren Schritte:
1. Zunächst startet man mit kleinen Flavors.
2. Dann evaluiert man die Performanz des geplanten Projektes mit diesem Flavor.
3. Treten Probleme auf, so wechselt man auf einen höheren Flavor.
 
## Flavors ändern

Der Wechsel auf einen anderen Flavor ist denkbar einfach:

1. Zuerst navigiert man in den gewünschten Cluster.

    <img src="clusters.png" width="1500" height="300"/>

2. Nun klickt man auf das Editieren-Icon derjenigen Node, deren Flavor man ändern möchte. Das Icon erscheint dabei erst dann, wenn man mit der Maus über die entsprechende Node fährt.

    <img src="node-selection.png" width="1500" height="700"/>

3. In dem jetzt geöffneten Fenster selektiert man dann den gewünschten Flavor und klickt zuletzt auf "Node Deployment editieren", um den Prozess abzuschließen.

    <img src="edit-node.png" width="600" height="700"/>

Kurz danach erscheint eine Bestätigungsnachricht auf Ihrem Bildschirm und der Flavor wurde erfolgreich geändert.