# Architektur und dokumentierter Bestand

Die Angaben stammen aus der bereitgestellten Architekturzeichnung und den ergänzenden Notizen. Stand der Aufbereitung: 6. September 2026. Dies ist keine Bestandsaufnahme des laufenden Hosts. Die Notizen enthalten Angaben zu einem Airflow-Datenbankkonto und zur Benutzeranlage, aber keinen Nachweis einer erfolgreichen Integration.

## Ressourcen

Die Bezeichnungen sind Rollen, keine realen Hostnamen oder VM-IDs.

| Rolle | vCPU | RAM laut Zeichnung (MB) | Disk laut Zeichnung (GB) | Betriebssystem laut Zeichnung |
|---|---:|---:|---:|---|
| Management / DevBox | 2 | 8192 | 70 | Ubuntu 24.04.4 LTS Desktop |
| Airflow | 1 | 4096 | 25 | Ubuntu 24.04.4 LTS Server |
| Spark Master | 1 | 2048 | 20 | Ubuntu 24.04.4 LTS Server |
| Spark Worker | 1 | 6144 | 30 | Ubuntu 24.04.4 LTS Server |
| PostgreSQL | 1 | 4096 | 40 | Ubuntu 24.04.4 LTS Server |
| Summe | 6 | 24576 | 185 | |

Die RAM-Einheit beim Abgleich mit Proxmox bestätigen: Falls MiB gemeint sind, entsprechen 24576 MiB genau 24 GiB. Hostbetrieb, Backups, Snapshots und freier Speicher benötigen zusätzliche Kapazität. Die Werte beschreiben den Bestand und sind keine Leistungszusage.

## Netzwerk

Die Zeichnung beschreibt eine gemeinsame Proxmox-Bridge, statische Gastadressen in einem /24-Netz, Gateway und DNS. Für die VMs ist kein externer Zugriff vermerkt. Routing und Firewall wurden nicht geprüft; eine Bridge allein stellt keine Isolation sicher.

Bridge, Subnetz, Gastadressen, Gateway, DNS, Hostnamen und freie VM-IDs werden für jede Zielumgebung neu zugeordnet. Auch ursprüngliche Adressendungen bleiben privat.

## Rollen und Datenfluss

Die DevBox dient Administration und Entwicklung. Airflow soll Workflows steuern, Spark verarbeitet Daten mit Master und Worker, PostgreSQL speichert relationale Daten. Die Zeichnung nennt außerdem Staging beziehungsweise temporäre Datenhaltung und einen möglichen Export nach Azure Blob Storage.

Beim Aufbau Airflow-Metadaten und fachliche Daten als getrennte Datenbanken und Rollen planen. Eine gemeinsame PostgreSQL-VM ist möglich. Konkrete Rechte, Airflow-Executor, Spark-Jobübergabe sowie Verteilung von DAGs und Job-Code sind noch offen.

## Fehlende Angaben für einen exakten Wiederaufbau

| Bereich | Zu erfassen |
|---|---|
| Proxmox | Version, Hostressourcen, Storage-Backend, VM-Firmware und Maschinentyp |
| Gäste | ISO-Prüfsummen, tatsächlicher Paketstand, Disk-Controller und Netzwerkkartenmodell |
| PostgreSQL | Version, Datenbanken, Rollenrechte, Listener und Authentifizierung |
| Airflow | Version, Python, Provider, Executor, Authentifizierungsmodell und Dienste |
| Spark | Version, Java/Python, Startart, Workerressourcen und Jobverteilung |
| Betrieb | Firewallregeln, Autostart, Zeitsynchronisation, Backup und Restore |

Echte Infrastrukturwerte ausschließlich privat ergänzen. Bereinigte Konfigurationen und nicht sensible Versionsangaben können später öffentlich ergänzt werden.
