Hier ist eine strukturierte Roadmap für das Purple Canary Pi-hole Plugin:

## Phase 1: Projektsetup (2-3 Stunden)

* [ ] GitHub-Repository erstellen mit Apache 2.0 oder GPL-3.0 Lizenz
* [ ] README.md mit Projektbeschreibung, Zielen und Hintergrund zu Pegasus/Spyware-Überwachung
* [ ] Basis-Ordnerstruktur anlegen: `/scripts`, `/config`, `/docs`, `/lists`
* [ ] Contributing Guidelines und Code of Conduct hinzufügen
* [ ] Issue-Templates für Bug Reports und Feature Requests


## Phase 2: IoC-Integration (3-4 Stunden)

* [ ] Script zum automatischen Fetch der AmnestyTech IoC-Listen von GitHub entwickeln
* [ ] Citizen Lab Domain-Listen identifizieren und integrieren
* [ ] Konvertierung in Pi-hole-kompatibles Format (domains-only Format)
* [ ] Update-Mechanismus mit Versionierung implementieren (täglich/wöchentlich check)
* [ ] Backup-Mechanismus für lokale Listen falls GitHub nicht erreichbar


## Phase 3: Query-Monitoring Engine (4-5 Stunden)

* [ ] Python/Bash-Script zur Überwachung der Pi-hole FTL-Datenbank (`/etc/pihole/pihole-FTL.db`)[^8_1]
* [ ] SQL-Query zur Erkennung von Treffern in den Spyware-Listen
* [ ] Logging-System für detektierte Ereignisse (Timestamp, Gerät, Domain, Query-Type)
* [ ] Deduplizierung um False-Positive-Spam zu vermeiden
* [ ] Systemd-Service oder Cronjob für kontinuierliches Monitoring


## Phase 4: Alert-System (3-4 Stunden)

* [ ] Integration mit ntfy.sh für Push-Benachrichtigungen (keine externe Abhängigkeit)
* [ ] Optional: E-Mail-Alerts via SMTP
* [ ] Optional: Gotify, Telegram, Slack Webhooks
* [ ] Konfigurierbare Alert-Schwellenwerte und Rate-Limiting
* [ ] Alert-Templates mit relevanten Kontext-Informationen (betroffenes Gerät, Domain, IoC-Quelle)


## Phase 5: Web-Dashboard (Optional, 6-8 Stunden)

* [ ] Einfaches HTML/JS-Dashboard als Pi-hole-Admin-Erweiterung
* [ ] Übersicht über detektierte Spyware-Queries (letzte 24h/7d/30d)
* [ ] Statistiken nach Quelle (AmnestyTech, Citizen Lab, etc.)
* [ ] Export-Funktion für Forensik (CSV/JSON)
* [ ] Integration mit Pi-hole-API für erweiterte Geräte-Informationen


## Phase 6: Installation \& Deployment (3-4 Stunden)

* [ ] Automatisches Installations-Script (`install.sh`) mit Dependency-Check
* [ ] Compatibility-Check für Pi-hole v5.x und v6.x
* [ ] Deinstallations-Script für sauberes Cleanup
* [ ] Docker-Container-Variante für Proxmox LXC/Docker-Setups
* [ ] Dokumentation: Schritt-für-Schritt-Anleitung mit Screenshots


## Phase 7: Testing \& Dokumentation (4-5 Stunden)

* [ ] Test-Suite mit simulierten Spyware-Domain-Lookups
* [ ] Dokumentation der Architektur und API
* [ ] Troubleshooting-Guide für häufige Probleme
* [ ] Datenschutz-Dokumentation (was wird geloggt, wo gespeichert)
* [ ] Security-Best-Practices (Logs verschlüsseln, sichere Alert-Kanäle)


## Phase 8: Community \& Outreach (2-3 Stunden)

* [ ] Blog-Post oder Ankündigung auf r/pihole, Hacker News
* [ ] Kontakt zu AmnestyTech und Citizen Lab für Feedback/Endorsement
* [ ] Translations: Mindestens EN/DE README
* [ ] Video-Tutorial oder Asciinema-Demo
* [ ] Monitoring der Issues und Community-Feedback

