* Warum ist ein Deployment in Kubernetes nicht einfach nur eine etwas andere Version von docker run mit --restart=always? 

A: Weil es nicht nur einen einzelnen Container startet, sondern eine ganze Anwendung verwaltet. Kubernetes sorgt dafür, dass immer die gewünschte Anzahl an Instanzen läuft, ersetzt fehlerhafte Container automatisch, erlaubt Updates ohne Ausfallzeit und kann die Anwendung bei Bedarf skalieren.

* Was tut das Deployment, wenn ein Pod plötzlich verschwindet – und warum ist das nicht einfach nur Magie? 

A: Wenn ein Pod plötzlich verschwindet, sorgt das Deployment dafür, dass automatisch ein neuer Pod gestartet wird, damit die gewünschte Anzahl wieder stimmt. Das ist keine Magie, weil Kubernetes ständig den Zustand der Anwendung überwacht. Es merkt, wenn etwas fehlt, und reagiert darauf – ganz nach den Regeln, die im Deployment festgelegt wurden.

* Was konntest du beim Rolling Update mit kubectl get pods -w beobachten – und wie wird hier sichergestellt, dass es keinen kompletten Ausfall gibt? 

A: Beim Rolling Update kannst du mit kubectl get pods -w beobachten, dass die alten Pods Stück für Stück ersetzt werden, ohne dass alle auf einmal abgeschaltet werden. Kubernetes startet zuerst die neuen Pods und wartet, bis sie laufen, bevor es die alten Pods beendet. Dadurch bleibt die Anwendung durchgehend verfügbar und es kommt zu keinem kompletten Ausfall.

* Wie sorgt der Kubernetes-Service dafür, dass dein Browser-Ping (über NodePort) den richtigen Pod trifft – selbst wenn sich gerade ein Update vollzieht? 

A: Der Kubernetes-Service verteilt die Anfragen des Browsers automatisch auf die aktuell laufenden Pods – auch während eines Updates.
Wenn ein Update läuft, schickt der Service keine Anfragen an Pods, die gerade neu gestartet werden oder noch nicht bereit sind. So landet der Ping immer bei einem funktionierenden Pod.

* In der Deployment-YAML: Welche Angaben betreffen die Pod-Vorlage, und welche regeln das Verhalten des Deployments (z.B. Skalierung, Strategie)? 

A: Die Pod-Vorlage legt fest, wie die Pods aussehen, und der Rest der Deployment-Konfiguration steuert, wie diese Pods verwaltet und skaliert werden.

* Was passiert mit den Pods, wenn du das Deployment löschst – und warum ist das Verhalten logisch?

A: Wenn du das Deployment löschst, verschwinden auch alle Pods, die dazu gehören. Das macht Sinn, weil die Pods vom Deployment erstellt und verwaltet werden. Ohne das Deployment gibt es keinen Grund mehr, die Pods am Leben zu erhalten, also werden sie ebenfalls gelöscht.