# Sichere Veröffentlichung

Öffentlich bleiben Rollen, Ressourcen, bereinigte Diagramme, Versionsangaben und Platzhalter. Reale Adressen einschließlich IPv6, DNS-Namen, Konten, E-Mail-Adressen, Passwörter, Tokens, Schlüssel, Verbindungszeichenfolgen und Cloud-Kennungen bleiben privat. Auch private LAN-Adressen werden nicht veröffentlicht.

Originaldokumente können Metadaten, Kommentare und Screenshots enthalten. Draw.io kann komplette Bilder einbetten. Sichtbare Adressen zu ersetzen reicht deshalb nicht aus. Das öffentliche Diagramm wird aus geprüften Rollen neu erstellt.

## Vor jedem Push

1. `git status --short` prüfen und nur gezielt Dokumentationsdateien stagen.
2. `git diff --cached --stat` und `git diff --cached` lokal prüfen.
3. Inhalte auf echte Adressen und Secrets prüfen; bei Binärdateien genügt Textsuche nicht.
4. Die gesamte zur Veröffentlichung vorgesehene Commitfolge prüfen, nicht nur den letzten Dateistand.
5. Danach den Dokumentationsbranch veröffentlichen und den GitHub-Diff prüfen.

`.gitignore` ist kein Secret-Scanner und entfernt keine bereits versionierten Inhalte oder früheren Commits. Private Inventare nicht mit `git add -f` hinzufügen. Rohmaterial und Backups bleiben außerhalb der Veröffentlichung.

## Bei einer Offenlegung

Betroffene Zugangsdaten ändern beziehungsweise widerrufen. Löschen aus einer Datei macht eine Offenlegung nicht rückgängig. Falls die Daten bereits auf GitHub liegen, Historie und weitere Kopien untersuchen und Bereinigung abstimmen. Niemals echte Secretwerte in Issues, Pull Requests oder Prüfprotokolle kopieren.
