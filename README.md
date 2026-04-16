# Data Engineering Homelab

Dieses Projekt dokumentiert die Konzeption und den Aufbau eines Proxmox-basierten Data-Engineering-Homelabs.  
Die Umgebung dient als praktische Lern- und Testplattform zur Simulation einer modularen Datenarchitektur mit getrennten Komponenten für Administration, Workflow-Orchestrierung, verteilte Datenverarbeitung und relationale Datenspeicherung.

## Projektziel

Ziel dieses Homelabs ist der Aufbau einer praxisnahen Umgebung für moderne Data-Engineering-Konzepte, insbesondere für:

- Infrastrukturplanung und Virtualisierung
- Linux-Server-Administration
- Workflow-Orchestrierung
- verteilte Datenverarbeitung
- relationale Datenspeicherung
- interne Netzwerk- und Servicekommunikation
- Vorbereitung zukünftiger ETL-, Analyse- und Cloud-Projekte

## Architekturübersicht

Das Homelab besteht aus mehreren virtuellen Maschinen mit klar getrennten Rollen:

| VM | Hostname | Rolle | Betriebssystem |
|---|---|---|---|
| VM1 | `mgmt-01` | Management / DevBox | Ubuntu 24.04 LTS Desktop |
| VM2 | `airflow-01` | Apache Airflow | Ubuntu 24.04 LTS Server |
| VM3 | `spark-master-01` | Apache Spark Master | Ubuntu 24.04 LTS Server |
| VM4 | `spark-worker-01` | Apache Spark Worker | Ubuntu 24.04 LTS Server |
| VM5 | `postgres-01` | PostgreSQL | Ubuntu 24.04 LTS Server |

## Kernkomponenten

### Management / DevBox
Die Management-VM dient als zentrale Verwaltungs- und Entwicklungsinstanz.  
Sie wird für SSH-Zugriffe, Datenbankadministration mit pgAdmin, Dokumentation sowie zukünftige Automatisierungsaufgaben verwendet.

### Apache Airflow
Airflow übernimmt die Orchestrierung von Workflows sowie die zeitliche Steuerung und Ausführung von Datenpipelines.

### Apache Spark
Spark wird in einer Master-/Worker-Struktur eingesetzt, um verteilte Datenverarbeitung und skalierbare Transformationsprozesse abzubilden.

### PostgreSQL
PostgreSQL dient als relationale Persistenzschicht für strukturierte Daten, Metadaten und zukünftige Projektergebnisse.

## Netzwerkdesign

Die Umgebung nutzt ein internes LAN auf Basis einer Proxmox-Bridge mit statischer IP-Adressierung.

| Hostname | IP-Adresse |
|---|---|
| `mgmt-01` | `192.x.x.20` |
| `airflow-01` | `192.x.x.21` |
| `spark-master-01` | `192.x.x.22` |
| `spark-worker-01` | `192.x.x.23` |
| `postgres-01` | `192.x.x.24` |

Die Kommunikation erfolgt ausschließlich innerhalb des internen Netzwerks. Öffentliche oder sensible Zugriffsdaten werden in diesem Repository nicht veröffentlicht.

## Generischer Datenfluss

Die Plattform folgt einem allgemeinen Data-Engineering-Flow:

1. Daten werden aus einer internen oder externen Quelle aufgenommen  
2. Apache Airflow orchestriert den Workflow  
3. Apache Spark verarbeitet und transformiert die Daten  
4. PostgreSQL speichert die erzeugten strukturierten Daten  
5. Gespeicherte Daten können anschließend für Analysen, Reports oder Folgeprozesse genutzt werden  

## Aktueller Umfang

Bereits umgesetzt oder vorbereitet:

- Proxmox-basierte VM-Architektur
- statisches internes Netzwerkdesign
- zentrale Management-VM
- PostgreSQL-Server-Setup
- Remotezugriff auf PostgreSQL über pgAdmin
- modulare Applikationsarchitektur
- generische Datenflussarchitektur

## Geplante nächste Schritte

- detaillierte Konfiguration von Apache Airflow
- Aufbau von Spark-Verarbeitungsworkflows
- Umsetzung der ersten End-to-End-Datenpipeline
- Entwicklung eines Wetterdaten-ETL-Projekts
- Erweiterung um Monitoring- und Visualisierungskomponenten
- spätere Übertragung einzelner Architekturelemente in Azure

## Zweck dieses Repositories

Dieses Repository dient zur Dokumentation von:

- Infrastrukturarchitektur
- Netzwerkarchitektur
- Applikationsarchitektur
- Datenflussarchitektur
- zukünftigen Data-Engineering-Projekten auf Basis der Plattform

## Hinweis

Dieses Repository enthält keine produktiven Zugangsdaten, geheimen Konfigurationswerte oder sensiblen internen Informationen.
