# iMKE Changelog v2.12.2

iMKE aktualisiert von v2.11.6 → v2.12.4

## Unterstützte Kubernetes Versionen:

Kubernetes-Cluster werden wie folgt aktualisiert, um Bugfixes und Sicherheitskorrekturen bereitzustellen.

v1.13.x -> v1.13.12
v1.14.x -> v1.14.8
v1.15.x -> v1.15.5

- Kunden können jetzt Kubernetes-Cluster mit Version 1.16.x erstellen.
- Das auslaufende Kubernetes 1.13 wurde entfernt.

## Wichtige neue Funktionen:

- Unterstützung für Kubernetes 1.16 wurde hinzugefügt
- K8S-Versionen, die von CVE-2019-11253 betroffen sind, wurden entfernt
- Möglichkeit hinzugefügt, Beschriftungen zu Projekten und Clustern hinzuzufügen und diese Beschriftungen an Knotenobjekte zu vererben.
- Unterstützung für die Kubernetes-Überwachungsprotokollierung hinzugefügt
- Die Schaltfläche "Verbinden" in den Clusterdetails öffnet jetzt das Kubernetes Dashboard
- Pod-Sicherheitsrichtlinien können jetzt aktiviert werden

## Instrumententafel:

- Das auslaufende Kubernetes 1.13 wurde entfernt.
- Neugestaltung des Dialogfelds zur Verwaltung von SSH-Schlüsseln im Cluster
- Redesign-Assistent: Zusammenfassung
- Das Umschalten des Clustertyps im Assistenten ist jetzt ausgeblendet, wenn nur ein Clustertyp aktiv ist
- Deaktivierte die Möglichkeit, neue Knotenbereitstellungen hinzuzufügen, bis der Cluster vollständig bereit ist.
- Der Clustername kann jetzt über das Dashboard bearbeitet werden
- Warnung über Änderungen der Knotenbereitstellung hinzugefügt, die alle Knoten neu erstellt.
- Die Pod-Sicherheitsrichtlinie kann jetzt über den Assistenten aktiviert werden
- Erweiterte Optionen im Assistenten überarbeitet
- Verschiedene Sicherheitsverbesserungen bei der Authentifizierung