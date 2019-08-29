---
title: Nutzungsrate der Cluster Nodes
body_classes: title-center title-h1h2
published: false
---

Während wir das Cluster geprüft haben ist uns eine ungewöhnliche Memory-Auslastung aufgefallen.
Es scheint so als ob ein Node komplett ausgelastet ist, während der zweite nur wenig Last zeigt.
Dies passiert oft, wenn ein Cluster mit weniger als drei Nodes ein Upgrade an den Nodes durchführt. 
Hier einmal grob erklärt, was passiert.


## Verbinden

Als erstes müssen wir wissen wie viele Nodes es gibt und wie die Auslastung ist.
![Step 1](get_top_node_1.png)

`Kubectl top node` zeigt die aktuelle Node Auslastung. Im Beispiel haben wie zwei Running(läuft ) Nodes. 

Erst wird der Node "cordoned" - also deaktiviert.

![Step 2](get_node_2.png)

Dann wird der Node "drained" - also komplett leer gemacht und Pods auf alle anderen Nodes verteilt.
Bei nur zwei Nodes wird also alles immer auf genau den einen anderen Node platziert.
![Step 3](top_node_3.png)

Wenn der zweite Node nach dem Update wieder läuft, werden die Pods _nicht_ automatisch auf beide Nodes verteilt. Dadurch kommt es zu dem eingangs beobachteten Ungleichgewicht.

## Hier ein paar Tipps:
Wir empfehlen mindestens drei Nodes zu verwenden, da so auch bei Updates Last besser verteilt werden kann.
Im Webterminal gibt es das Tool `popeye`, welches Hinweise auf Best Practices gibt: https://docs.imke.cloud/de/guides/webterminal.
Upgraden Sie die Nodes auf die neueste Version und beachten Sie den letzten Schritt in folgendem Guide: https://docs.imke.cloud/de/guides/upgradingacluster.
