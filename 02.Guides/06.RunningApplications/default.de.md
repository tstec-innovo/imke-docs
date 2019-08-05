---
title: Eine Anwendung in Kubernetes starten
body_classes: title-center title-h1h2
published: true
---

Das Cluster läuft und nun wollen wir eine Applikation
betreiben. Als Beispiel verwenden wir einen nginx, der
per Load Balancer vor dem Cluster veröffentlicht wird.

## Vorraussetzungen

Damit diese Anleitung funktioniert sind foldenge Dinge
Vorraussetzung. Um die Vorbereitungszeit zu verkürzen
kann alternativ das iMKE Web Terminal verwendet werden.
Dieses erfüllt die folgende Liste.

* `kubectl` in Version > `1.13`
* ein laufendes Kubernetes Cluster
* eine aktive `kubeconfig`

## Datentypen

### Deployment

### Service

## Manifeste

Um nginx auf Kubernetes laufen zu lassen brauchen wir
als erstes ein Objekt vom Typ `Deployment`. Dies lässt
sich mittels `kubectl` leicht generieren.

```bash
kubectl create deployment --dry-run -o yaml --image nginx nginx

apiVersion: apps/v1
kind: Deployment
metadata:
  creationTimestamp: null
  labels:
    app: nginx
  name: nginx
spec:
  replicas: 1
  selector:
    matchLabels:
      app: nginx
  strategy: {}
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: nginx
    spec:
      containers:
      - image: nginx
        name: nginx
        resources: {}
status: {}
```

Dies sieht schon sehr gut aus. Dies speichern wir nun in eine Datei
deployment.yaml

```bash
kubectl create deployment --dry-run -o yaml --image nginx nginx > deployment.yaml
```

Als nächstes benötigen wir einen Service, der die Applikation von
der Öffentlichkeit aus zugänglich macht. Als Typ wählen wir
`LoadBalancer`, dies erstellt in OpenStack direkt einen fertig
konfigurierten LoadBalancer als Einstieg in das Cluster.

```bash
kubectl create service loadbalancer --dry-run --tcp=80 -o yaml nginx

apiVersion: v1
kind: Service
metadata:
  creationTimestamp: null
  labels:
    app: nginx
  name: nginx
spec:
  ports:
  - name: "80"
    port: 80
    protocol: TCP
    targetPort: 80
  selector:
    app: nginx
  type: LoadBalancer
status:
  loadBalancer: {}
```

Auch dies speichern wir nun wieder in eine Datei, dieses Mal `service.yaml`

```bash
kubectl create service loadbalancer --dry-run --tcp=80 -o yaml nginx > service.yaml
```

Diese zwei Dateien sind die Grundlage für ein öffentliches nginx in Kubernetes.
Zusammen gehören diese zwei Manifeste nicht. Die einzige Verbindung ist das Label
`app: nginx`, welches das Deployment in den Metadaten und der Service als Selektor
definiert hat. 

## Erstellen der Applikation

Nun müssen wir die zwei Dateien an die Kubernetes API schicken.

```bash
kubectl apply -f deployment.yaml
deployment.apps/nginx created

kubectl apply -f service.yaml
service/nginx created
```

Nun können wir uns die zwei erstellten Objekte anschauen.

```bash
kubectl get deployment,service
NAME                          READY   UP-TO-DATE   AVAILABLE   AGE
deployment.extensions/nginx   1/1     1            1           55s

NAME                 TYPE           CLUSTER-IP    EXTERNAL-IP   PORT(S)         AGE
service/kubernetes   NodePort       10.10.10.1    <none>        443:31630/TCP   2d23h
service/nginx        LoadBalancer   10.10.10.86   <pending>     80:31762/TCP    46s
```

Wie ersichtlich wurde das Deployment angelegt und ist im Zustand READY.
Der Service nginx wurde auch angelegt, die EXTERNAL-IP ist jedoch noch
`pending`. Hier müssen wir nun ein bisschen warten bis der LoadBalancer
provisioniert wurde.

Nach etwa 1-2 Minuten kann man das Kommando erneut ausführen und bekommt
nun eine IP angezeigt:

```bash
kubectl get deployment,svc
NAME                          READY   UP-TO-DATE   AVAILABLE   AGE
deployment.extensions/nginx   1/1     1            1           2m8s

NAME                 TYPE           CLUSTER-IP    EXTERNAL-IP       PORT(S)         AGE
service/kubernetes   NodePort       10.10.10.1    <none>            443:31630/TCP   2d23h
service/nginx        LoadBalancer   10.10.10.86   185.116.245.169   80:31762/TCP    119s
```

Die External IP `185.116.245.169`aus unserem Beispiel ist nun öffentlich
erreichbar und zeigt unsere Instanz von nginx an.

## Aufräumen

Das ganze kann sehr einfach nun auch wieder gelöscht werden.

```bash
kubectl delete -f service.yaml
service "nginx" deleted

kubectl delete -f deployment.yaml
deployment.apps "nginx" deleted

kubectl get deployment,svc

NAME                 TYPE       CLUSTER-IP   EXTERNAL-IP   PORT(S)         AGE
service/kubernetes   NodePort   10.10.10.1   <none>        443:31630/TCP   2d23h
```

Wie man sieht ist alles wieder weg und im Browser aktualisieren wird auch
einen Fehler anzeigen. Die Applikation läuft nicht mehr.

## Zusammenfassung

Folgende Schritte wurden erfolgreich durchgeführt und gelernt:

* Wie spreche ich mit Kubernetes
* Was ist ein Deployment
* Wie lege ich ein Deployment an
* Was ist ein Service
* Wie lege ich einen Service an
* Wie lösche ich die Applikation wieder

Herzlichen Glückwunsch! Dies sind alle notwendigen Schritte, um in Kubernetes
Applikationen zu starten.
