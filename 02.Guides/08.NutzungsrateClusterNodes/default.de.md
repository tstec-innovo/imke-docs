---
title: Nutzungsrate der Cluster Nodes
body_classes: title-center title-h1h2
published: false
---

Bei der Überprüfung des Clusters ist uns eine ungewöhnlich hohe Speicher-Auslastung aufgefallen.
Wir sehen, dass ein Node komplett ausgelastet ist, während der andere nur wenig Last zeigt.
Dies passiert oft, wenn bei einem  Cluster mit weniger als drei Nodes ein Upgrade an den Nodes durchgeführt wird. 
Hier erklären wir einmal, wie es dazu kommt.


## Node Auslastung

Als erstes schauen wir, wieviele Nodes im Cluster sind, und wie ihre Auslastung ist.
![Step 1](get_top_node_1.png)

Der Befehl `kubectl top node` zeigt die aktuelle Node Auslastung. Im Beispiel haben wie zwei Running (laufende) Nodes. 

Erst wird der Node "cordoned" - also deaktiviert, damit keine neuen Pods auf dem Node gestartet werden.


![Step 2](get_node_2.png)

Dann wird der Node "drained" - also komplett leer gemacht und die bisher auf dem gedrainten Node laufenden Pods auf alle anderen Nodes des Clusters verteilt.
Bei nur zwei Nodes wird also alles immer auf genau den einen anderen Node platziert.
![Step 3](top_node_3.png)

Wenn der zweite Node nach dem Update wieder läuft, werden die Pods _nicht_ automatisch auf beide Nodes verteilt. Dadurch kommt es zu dem eingangs beobachteten Ungleichgewicht.

## Hier ein paar Tipps:
Wir empfehlen mindestens drei Nodes zu verwenden, da so auch bei Upgrades Last besser verteilt werden kann.
Im Webterminal gibt es das Tool `popeye`, welches den Cluster analysiert und Verbesserungs-Vorschläge auf Grundlage von  Best Practices macht: https://docs.imke.cloud/de/guides/webterminal.
Upgraden Sie die Nodes auf die neueste Version und beachten Sie den letzten Schritt in folgendem Guide: https://docs.imke.cloud/de/guides/upgradingacluster.
