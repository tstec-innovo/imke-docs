---
title: Cluster Update
body_classes: title-center title-h1h2
published: true
---

Sicherheit des Clusters steht an erster Stelle, hinzu
kommen noch einige neue Features mit jedem Release. Um
hier auf der sicheren und modernen Seite zu sein empfieht
es sich regelmässig Updates zu installieren.

In besonders kritischen Fällen updaten wir die Cluster API
automatisch auf die letzte Minor-Version um auch unsere eigene
Infrastruktur sicher zu halten. In diesem Fall kann der nächste
Block übersprungen werden. Nodes müssen dann nämlich dennoch
selbst geupdated werden.

## Der Cluster

In Kubernetes teilt sich die Infrastruktur in Master und Nodes.
Bei iMKE Clustern werden die Master verwaltet.

Da mehrere Versionen für die Master angeboten werden, hat man
hier im Webinterface von iMKE die Wahl der Version offen. Ein
Update der Master ist mit ein paar Mausklicks erledigt.

Als erstes gehen wir in den Cluster, den wir updaten wollen.
![Step 1](update_1.png)

Nun klicken wir in das Feld `Master Version` und wählen eine
neue Version für die Master.
![Step 2](update_2.png)

Jetzt aktualisiert iMKE die Master selbstständig und wir sind mit
diesem Schritt fertig.

## Die Nodes

Nachdem die Master ihr Update vollzogen haben müssen wir nun noch
die Nodes aktualisieren. Auch hier hilft uns das iMKE Webinterface.
Es ist jedoch zu beachten, dass bei einem Update neue Nodes erzeugt
und die alten Nodes gelöscht werden. Dabei werden zwangsweise auch
alle Pods neu gestartet.

Als ersten Schritt klicken wir nun auf das Node Deployment.
![Step 3](update_3.png)

Nun clicken wir auf dem Bleistift Symbole, um die Update-Ansicht
aufzumachen.
![Step 4](update_4.png)

Bei kubelet Version wählen wir nun die Version aus, welche auch bei
unserem Cluster Master konfiguriert ist. In diesem Beispiel
`1.15.3` und bestätigen mit `Edit Node Deployment`
![Step 5](update_5.png)

Nun wird iMKE automatisch die Node Group auf die neue Version
aktualisieren und Kubernetes dafür sorgen, dass unsere Applikationen
neu auf die neuen aktualisierten Nodes verteilt werden.

## Zwei Node Cluster

Aufzupassen ist hier mit Clustern mit zwei Nodes. iMKE nutzt ein
rollierendes Update als Strategie für das Update. Hierbei wird immer
ein Node nach dem anderen getauscht. Bei einem Cluster mit zwei oder
weniger Nodes bedeutet dies, dass der zuerst geupdatete Node komplett
voll geplant wird, noch bevor der zweite fertig ist.

Als Lösung gibt es ein recht einfaches Bash-Script, welches in einem
Namespace alle Pods noch einmal neu erstellen lässt: 
https://github.com/truongnh1992/playing-with-istio/blob/master/upgrade-sidecar.sh

Dieses nutzen wir, sobald das Cluster komplett geupdated ist im
WebTerminal.

```bash
curl -o upgrade-node.sh https://raw.githubusercontent.com/truongnh1992/playing-with-istio/master/upgrade-sidecar.sh
chmod +x upgrade-node.sh
echo -e "#\!/bin/bash\n$(cat upgrade-node.sh)" > upgrade-node.sh
```

Nun müssen wir nur noch dieses Script auf alle unsere Namespaces anwenden.

```bash
kubectl get namespace
NAME              STATUS   AGE
default           Active   36m
kube-node-lease   Active   36m
kube-public       Active   36m
kube-system       Active   36m
webterminal       Active   4m42s

# Wir interessieren uns also für default
./upgrade-node.sh default

Refreshing pods in all Deployments
```

Nun sind auch alle Pods sauber neu auf unsere Nodes verteilt worden.
