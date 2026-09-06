# Wiederaufbau und Abnahme

Diese Anleitung überträgt den dokumentierten Bestand in eine neue Umgebung. Sie ist noch kein getestetes Installationsskript. Unbekannte Versionen und Einstellungen vor der Installation ergänzen und Abweichungen dokumentieren.

## 1. Inventar vorbereiten

`config/environment.example.yaml` nach `private/environment.yaml` kopieren und alle Platzhalter lokal ersetzen. Zugangsdaten getrennt im Passwortmanager ablegen. Die YAML-Datei dokumentiert Zuordnungen; sie führt kein Deployment aus.

Subnetzkonflikte, freie VM-IDs, Bridge und Storage prüfen. Ressourcen aus der Architekturübersicht plus Reserve für Host und Backups bereitstellen. Vor Änderungen an bestehenden Systemen eine Sicherung erstellen.

## 2. Proxmox und Ubuntu

1. Proxmox-Version, Storage, Installationsmedien und Prüfsummen festhalten.
2. Bridge, Gastnetz, Gateway und DNS festlegen; Verwaltungszugang vor Netzwerkänderungen absichern.
3. Fünf VMs gemäß Ressourcentabelle anlegen. Freie lokale IDs, Firmware, Controller und Netzwerkkartenmodell im privaten Inventar erfassen.
4. Ubuntu Desktop für Management und Ubuntu Server für die übrigen Rollen installieren. Dokumentierter Ausgangsstand: 24.04.4 LTS. Updates und Abweichungen festhalten.
5. Administration, SSH-Schlüssel, statische Adressierung, DNS und Zeitsynchronisation einrichten und prüfen.
6. Falls verwendet, QEMU Guest Agent im Gast installieren und in Proxmox aktivieren; Kommunikation prüfen.

## 3. PostgreSQL

Version ermitteln und für den Neuaufbau festlegen. Datenbank und eingeschränkte Rolle für Airflow-Metadaten sowie getrennte Rollen für fachliche Daten anlegen. Passwörter interaktiv oder über geschützte Secret-Verwaltung setzen.

Listener, Authentifizierung und Firewall auf benötigte Clients begrenzen. Zugriff von Airflow und gegebenenfalls der DevBox testen. Ein nicht zugelassener Client muss abgewiesen werden. Keine Verbindungszeichenfolgen mit Zugangsdaten veröffentlichen.

## 4. Spark

Kompatible Spark-, Java- und gegebenenfalls Python-Versionen festlegen. Master starten, Worker registrieren und dessen Ressourcen passend zur VM begrenzen. Startverfahren und Jobverteilung dokumentieren. Registrierung, kleinen Testjob und Neustartverhalten prüfen. Die konkrete Dienstkonfiguration ist im aktuellen Bestand noch nicht belegt.

## 5. Airflow

Airflow-, Python- und Provider-Versionen sowie Executor festlegen. Eine isolierte Python-Umgebung mit zur Airflow-Version passenden Constraints verwenden; siehe [offizielle Installationsanleitung](https://airflow.apache.org/docs/apache-airflow/stable/installation/installing-from-pypi.html). Eine unversionierte Installation ist kein reproduzierbarer Stand.

Private Datenbankverbindung konfigurieren. Initialisierung beziehungsweise Migration, Authentifizierung und Dienststart nach der Dokumentation der ausgewählten Version durchführen. Der Benutzeranlage-Befehl aus den Originalnotizen wird nicht übernommen, weil Version und Authentifizierungsmodell nicht belegt sind.

Einen minimalen DAG testen und anschließend Spark anbinden. Festhalten, wo Job-Code liegt und wie Worker und gegebenenfalls Driver darauf zugreifen. Erst nach erfolgreichem Test die Integration als umgesetzt markieren.

## 6. Abnahme

- [ ] Fünf VMs starten mit der vorgesehenen Ausstattung.
- [ ] DNS, Uhrzeit und erlaubte Verwaltungszugriffe funktionieren.
- [ ] PostgreSQL akzeptiert nur vorgesehene Clients und Rollen.
- [ ] Spark registriert den Worker und führt einen Testjob aus.
- [ ] Airflow lädt einen Test-DAG und erreicht die Metadatenbank.
- [ ] Eine kleine synthetische Datenmenge durchläuft die Pipeline mit geprüftem Ergebnis.
- [ ] Dienste kommen nach kontrolliertem Neustart wieder hoch.
- [ ] Backup wurde isoliert wiederhergestellt und geprüft.

## 7. Backup und Restore

VM-Backups nach dem [Proxmox-Backupkonzept](https://pve.proxmox.com/pve-docs/chapter-vzdump.html) planen. Für PostgreSQL ein konsistentes Datenbankbackup und Restoreverfahren festlegen. Backups und benötigte Entschlüsselungsschlüssel privat aufbewahren. Ein Snapshot allein ersetzt kein unabhängiges Backup.

Restore zuerst in einem isolierten Netz durchführen, damit keine doppelten Adressen entstehen. Ziel-IDs, Storage und Netzwerkzuordnung prüfen. Anschließend die Abnahme wiederholen. Datum, Versionsstand, Dauer und Abweichungen ohne private Werte dokumentieren.
