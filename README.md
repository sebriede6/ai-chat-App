```markdown
# AI Chat App - Helm Exercise

Dieses Projekt demonstriert die grundlegenden Schritte zur Verwendung von Helm als Paketmanager für Kubernetes.
Es wurde ein einfaches Helm-Chart für eine Nginx-Anwendung erstellt, installiert, aktualisiert und deinstalliert.

**Verzeichnisstruktur:**
    *  
        ```
        DeinProjekt/
        ├── README.md
        ├── assets/
        │   ├── screenshot
        │   ├── screenshot
        │   ├── screenshot
        │   ├── screenshot
        │   ├── screenshot
        │   └── screenshot
        ├── helm-exercise/
        │   ├── charts/
        │   │   └── my-first-helm-chart/
        │   │       ├── Chart.yaml
        │   │       ├── values.yaml
        │   │       └── templates/
        │   │           └── ...
        └── ... (andere Projektdateien)
        ```


## Aufgabe

Ziel dieser Übung war es, den grundlegenden Helm-Workflow zu erlernen:
1.  Ein neues Helm-Chart erstellen.
2.  Die Struktur eines Helm-Charts verstehen (Chart.yaml, values.yaml, templates/).
3.  Ein Chart als Release in einem lokalen Kubernetes-Cluster installieren.
4.  Einen bestehenden Release durch Ändern von Konfigurationswerten aktualisieren.
5.  Einen Helm-Release und alle zugehörigen Kubernetes-Objekte deinstallieren.

## Voraussetzungen

*   Docker ist installiert und läuft.
*   `kubectl` ist installiert und mit einem lokalen Kubernetes-Cluster verbunden (z.B. Docker Desktop Kubernetes, Minikube, Kind).
*   Helm CLI ist installiert.

## Erstellung und Management des Helm Charts

Das Helm Chart `my-first-helm-chart` befindet sich im Verzeichnis `helm-exercise/charts/my-first-helm-chart/`.

### 1. Chart Erstellung

Ein neues Helm Chart wurde mit dem folgenden Befehl erstellt (aus dem Verzeichnis `helm-exercise/charts/`):
```bash
helm create my-first-helm-chart
```
Dies generiert ein Standard-Chart für eine Nginx-Anwendung.

### 2. Chart Installation

Das Chart wurde als Release namens `my-nginx-release` im `default` Namespace installiert:
```bash
# Navigiere in das Verzeichnis über dem Chart (helm-exercise/charts/)
helm install my-nginx-release my-first-helm-chart/
```

### 3. Release Überprüfung (Initial)

Der Status des Releases und die erstellten Kubernetes-Objekte wurden überprüft:
```bash
helm list
kubectl get all -l app.kubernetes.io/instance=my-nginx-release
```
Zugriff auf die Nginx-Anwendung erfolgte via Port-Forwarding:
```bash

kubectl port-forward service/<service-name> 8080:80
```
Anschließend wurde `http://localhost:8080` im Browser aufgerufen.

### 4. Release Aktualisierung (Upgrade)

Die Konfiguration wurde geändert, indem `replicaCount` in `helm-exercise/charts/my-first-helm-chart/values.yaml` von `1` auf `3` gesetzt wurde.
Der Release wurde mit den neuen Werten aktualisiert:
```bash
helm upgrade my-nginx-release my-first-helm-chart/
```
Die Aktualisierung der Deployments wurde überprüft:
```bash
kubectl get deployment -l app.kubernetes.io/instance=my-nginx-release
```

### 5. Release Deinstallation

Der Release und alle zugehörigen Kubernetes-Objekte wurden entfernt:
```bash
helm uninstall my-nginx-release
```

### 6. Überprüfung der Deinstallation

Es wurde sichergestellt, dass der Release und die Objekte nicht mehr existieren:
```bash
helm list
kubectl get all -l app.kubernetes.io/instance=my-nginx-release
```

## Screenshots der Durchführung

Die folgenden Screenshots dokumentieren die erfolgreiche Durchführung der oben genannten Schritte.


    ![Screenshots](./assets/)


---

```

