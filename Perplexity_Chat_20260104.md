# Frage: Indicators of Compromise, Pegasus

**Frage:** Was sind die "Indicators of compromise" mit Pegasus spyware? Wurden die Angriffsvektoren identifiziert und Indikatoren von NGOs veröffentlicht, die einem helfen, eine Kompromittierung von Geräten zu identifizieren?

**Antwort:** Pegasus ist eine hochentwickelte Spyware der israelischen Firma NSO Group, die iOS- und Android-Geräte kompromittieren kann. Die Angriffsvektoren wurden identifiziert und Amnesty International hat umfassende Indikatoren (Indicators of Compromise, IoCs) veröffentlicht, um eine Infektion nachzuweisen.[^1_1][^1_2][^1_3][^1_4]

## Identifizierte Angriffsvektoren

Die Pegasus-Spyware nutzt mehrere Infektionsmethoden:[^1_5][^1_6]

- **Zero-Click-Exploits**: Die ausgeklügeltste Methode, bei der keine Benutzerinteraktion erforderlich ist. Pegasus nutzt Zero-Day-Schwachstellen in iMessage, WhatsApp, Apple Music und der iOS Photos-App aus[^1_2][^1_3][^1_5]
- **Network Injection**: Angreifer leiten Netzwerkverkehr über kompromittierte Mobilfunkbetreiber oder taktische Geräte (Rogue Cell Towers) um und injizieren Schadsoftware[^1_2]
- **Spear-Phishing**: Die ursprüngliche Methode (2016) nutzte manipulierte SMS-Nachrichten mit bösartigen Links[^1_5]
- **Push-Notification-Exploits**: Ausnutzung des Push-Benachrichtigungssystems zur Codeausführung[^1_6]


## Indicators of Compromise (IoCs)

Amnesty International hat detaillierte forensische Indikatoren dokumentiert:[^1_4][^1_2]

### Technische Indikatoren auf iOS-Geräten

- **Verdächtige Prozesse**: Spezifische Prozessnamen wie `bh` (BridgeHead), `roleaccountd`, `msgacntd`, `pcsd`, `fmld`, `stagingd`, die keine legitimen iOS-Binaries sind[^1_2]
- **Datenbank-Anomalien**: Inkonsistenzen in den SQLite-Datenbanken `DataUsage.sqlite` und `netusage.sqlite`, wo Prozessnamen gelöscht wurden, aber Einträge in der ZLIVEUSAGE-Tabelle verbleiben[^1_2]
- **Verdächtige Domains**: Über 700 Pegasus-bezogene Domains wie `free247downloads[.]com`, `urlpush[.]net`, `opposedarrangement[.]net`[^1_2]
- **iMessage-Lookups**: Unbekannte iCloud-Accounts in `/private/var/mobile/Library/Preferences/com.apple.identityservices.idstatuscache.plist`[^1_2]
- **Shutdown.log-Anomalien**: Kaspersky entdeckte 2024 eine Methode zur Erkennung über die `shutdown.log`-Datei, die Neustarts protokolliert[^1_3][^1_7]


### Sichtbare Symptome

Benutzer können folgende Anzeichen bemerken:[^1_1]

- Ungewöhnlich hoher Akkuverbrauch
- Unerwartete Datennutzungsspitzen
- Performance-Probleme und Lags
- Unbefugter Zugriff auf Mikrofon oder Kamera ohne Benutzererlaubnis


## Veröffentlichte Tools und Ressourcen von NGOs

Amnesty International hat mehrere Ressourcen zur Verfügung gestellt:[^1_8][^1_4][^1_2]

- **Mobile Verification Toolkit (MVT)**: Ein Open-Source-Forensiktool, das Backup-Dateien auf Kompromittierungsindikatoren analysiert[^1_8]
- **GitHub-Repository**: Das AmnestyTech/investigations-Repository enthält IoCs aus technischen Untersuchungen gegen Menschenrechtsverteidiger[^1_9][^1_1]
- **Forensic Methodology Report**: Ein detaillierter Bericht, der die forensischen Spuren auf iOS- und Android-Geräten nach Pegasus-Angriffen dokumentiert[^1_2]

Die Erkenntnisse zeigen, dass NSO Group-Kunden bis Juli 2021 in der Lage waren, alle aktuellen iPhone-Modelle und iOS-Versionen, einschließlich vollständig gepatchter Geräte, remote zu kompromittieren.[^1_2]
<span style="display:none">[^1_10]</span>

[^1_1]: https://www.huntress.com/threat-library/malware/pegasus-malware

[^1_2]: https://www.amnesty.org/en/latest/research/2021/07/forensic-methodology-report-how-to-catch-nso-groups-pegasus/

[^1_3]: https://en.wikipedia.org/wiki/Pegasus_(spyware)

[^1_4]: https://www.business-humanrights.org/de/neuste-meldungen/amnesty-internationals-forensic-methodology-report-how-to-catch-nso-groups-pegasus/

[^1_5]: https://blog.qualys.com/vulnerabilities-threat-research/2021/07/23/protect-your-devices-from-pegasus-spyware-using-vmdr-for-mobile-devices-proactive-approach

[^1_6]: https://us.norton.com/blog/emerging-threats/pegasus-spyware

[^1_7]: https://iverify.io/blog/key-iocs-for-pegasus-and-predator-spyware-cleaned-with-ios-26-update

[^1_8]: https://surfshark.com/blog/pegasus-spyware

[^1_9]: https://github.com/AmnestyTech/investigations

[^1_10]: https://www.amnesty.org/en/wp-content/uploads/2021/08/DOC1044872021ENGLISH.pdf


---

# Filter-Regeln in PiHole?
**Frage:** Gibt es Filter in PiHole, die beim Aufruf von entsprechenden Sites Alarm schlagen? Als eine Art Kanarienvogel?

**Antwort:** Ja, es gibt spezifische Blocklisten für Pi-hole, die Pegasus-Spyware-Domains enthalten und als eine Art Frühwarnsystem fungieren können. Diese Listen basieren auf den von Amnesty International veröffentlichten Indikatoren (IoCs).[^2_1]

## Verfügbare Pegasus-Blocklisten für Pi-hole

Die Community hat die Amnesty International IoCs in Pi-hole-kompatible Blocklisten umgewandelt. Das AmnestyTech GitHub-Repository enthält mehrere Domain-Listen, die direkt in Pi-hole importiert werden können:[^2_1]

- **domains.txt**: Die Hauptliste, die alle anderen Listen (domains_v2, v3, v4) kombiniert und somit die umfassendste Option darstellt[^2_1]
- **domains_v2.txt, domains_v3.txt, domains_v4.txt**: Separate Listen aus verschiedenen Untersuchungszeiträumen
- **domains_v4_validation.txt**: Spezielle Validierungsliste

Die Empfehlung ist, die **domains.txt** zu verwenden, da sie alle anderen Listen bereits enthält.[^2_1]

## Funktionsweise als Kanarienvogel

Wenn ein Gerät in deinem Netzwerk versucht, eine der geblockten Pegasus-Domains zu kontaktieren, wird diese Anfrage von Pi-hole blockiert und in den Query-Logs dokumentiert. Du kannst im Pi-hole-Webinterface unter "Query Log" alle DNS-Anfragen überwachen und nach blockierten Domains filtern.[^2_5][^2_6]

## Wichtige Einschränkungen

Es gibt jedoch zwei kritische Limitierungen:[^2_1]

- **Keine Zukunftssicherheit**: Die Listen schützen nur gegen bereits bekannte Pegasus-Domains. Neue Versionen der Spyware mit neuen Command-and-Control-Servern werden nicht erkannt
- **Historische Daten**: Die Listen enthalten hauptsächlich Domains aus vergangenen Angriffen, die möglicherweise nicht mehr aktiv sind


## Integration in Pi-hole

Du kannst die Listen einfach über das Webinterface hinzufügen:[^2_6][^2_5]

1. Navigiere zu `Lists` im Pi-hole-Menü
2. Füge die URL der domains.txt aus dem AmnestyTech GitHub-Repository hinzu
3. Weise die Liste einer Gruppe zu (Standard: Default)
4. Führe ein manuelles Update der Gravity-Listen durch

Für zusätzliche Überwachung könntest du das Query-Logging aktivieren und regelmäßig nach blockierten Pegasus-Domains suchen. Dies bietet zwar keinen vollständigen Schutz, kann aber als zusätzliche Sicherheitsebene und Frühwarnsystem gegen bekannte Spyware-Infrastruktur dienen.[^2_3][^2_6]
<span style="display:none">[^2_2][^2_4][^2_7][^2_8][^2_9]</span>

[^2_1]: https://www.reddit.com/r/pihole/comments/opmrgw/nsopegasus_blocklist/

[^2_2]: https://www.youtube.com/watch?v=JPCQnHgvIhI

[^2_3]: https://docs.pi-hole.net/ftldns/configfile/

[^2_4]: https://discourse.pi-hole.net/t/richtige-und-sichere-dns-einstellungen/29026

[^2_5]: https://www.elefacts.de/test-neue_ad_block_filterlisten_in_pi_hole_einbinden

[^2_6]: https://www.kuketz-blog.de/pi-hole-einrichtung-und-konfiguration-mit-fritzbox-adblocker-teil1/

[^2_7]: https://www.crosstalksolutions.com/the-worlds-greatest-pi-hole-and-unbound-tutorial-2023/

[^2_8]: https://www.youtube.com/watch?v=Aisa8qAjllc

[^2_9]: https://www.computerbase.de/forum/threads/pihole-einstellung-methoden-und-filterlisten.1978703/page-2


---

# Pflege von Filterregeln für Spyware-Indikatoren?
**Frage:** Es gibt niemanden bei einer NGO, der/die sich die Pflege einer solchen Liste auf die Fahnen geschrieben hat? Wenn ich das richtig sehe, dann wird AI (und vermutlich andere) die Liste auf GitHub doch pflegen, oder? Entsprechend könnte man das doch mit einem Dienst verbinden, oder? Wie hoch wäre der Aufwand?

**Antwort:** Du hast recht - Amnesty International (AmnestyTech) pflegt das GitHub-Repository mit den Pegasus-IoCs aktiv weiter. Auch das Citizen Lab an der University of Toronto dokumentiert kontinuierlich neue NSO-Group-Spyware-Fälle und veröffentlicht technische Indikatoren. Die neuesten Veröffentlichungen von Amnesty International zeigen Pegasus-Fälle aus März 2025 in Serbien mit aktualisierten technischen Details.[^3_1][^3_2][^3_3][^3_4]

## Automatisierung mit Pi-hole

Die Integration ist technisch relativ einfach umzusetzen. Pi-hole unterstützt von Haus aus externe Blocklisten über URLs, die bei jedem Gravity-Update (standardmäßig wöchentlich) automatisch aktualisiert werden. Der Aufwand ist minimal:[^3_5][^3_6]

### Einfache Lösung (Low Effort)

- AmnestyTech GitHub-URLs direkt in Pi-hole als Adlist eintragen
- Pi-hole lädt bei jedem wöchentlichen Gravity-Update automatisch die neueste Version
- **Aufwand**: 5-10 Minuten für die initiale Einrichtung, danach vollautomatisch


### Erweiterte Lösung mit Monitoring

Du könntest ein automatisiertes System mit zusätzlicher Alarmierung aufsetzen:[^3_5]

1. **Automatisches Update**: Tools wie `pihole-updatelists` ermöglichen erweiterte Automatisierung mit Fehlerbehandlung[^3_5]
2. **Alert-System**: Ein Python/Bash-Script, das Pi-hole Query-Logs überwacht und bei Treffern in den Pegasus-Listen Alarm schlägt (z.B. per E-Mail, Telegram, ntfy.sh)
3. **Aufwand**: 2-4 Stunden für die Entwicklung eines Monitoring-Scripts plus Cronjob-Einrichtung

### Technische Herausforderung

Das Hauptproblem liegt nicht in der technischen Umsetzung, sondern in der Natur der Bedrohung: Die IoC-Listen enthalten hauptsächlich historische Domains aus bereits dokumentierten Angriffen. NSO Group und ähnliche Anbieter ändern ihre Infrastruktur regelmäßig, sodass neue Angriffswellen mit neuen Domains stattfinden, die erst nach forensischer Analyse durch Amnesty oder Citizen Lab dokumentiert werden.[^3_2][^3_7][^3_4]

Die Automation wäre also ein reaktives System - es warnt vor bekannten Indikatoren, bietet aber keinen proaktiven Schutz gegen Zero-Day-Exploits oder neue C2-Infrastruktur. Dennoch ist es als zusätzliche Sicherheitsebene und zur Dokumentation verdächtiger Aktivitäten im Netzwerk wertvoll.[^3_7]
<span style="display:none">[^3_10][^3_8][^3_9]</span>

[^3_1]: https://github.com/AmnestyTech/investigations

[^3_2]: https://www.amnesty.org/es/wp-content/uploads/2025/03/EUR7091862025ENGLISH.pdf

[^3_3]: https://dawnmena.org/citizenlab-reports-jordan-used-nso-group-spyware-to-hack-activists-devices/

[^3_4]: https://issues.org/surveillance-spyware-uso-group-pegasus-citizen-lab/

[^3_5]: https://github.com/jacklul/pihole-updatelists

[^3_6]: https://gist.github.com/andreacioni/8b4662f551ce3e2b052905977bb7ea30

[^3_7]: https://foresiet.com/blog/pegasus-spyware-november-2025-a-deep-dive-into-shadowy-surge-and-the-global-surveillance-crisis/

[^3_8]: https://www.bindmans.com/news-insights/news/bindmans-continue-to-investigate-potential-pegasus-malware-claims/

[^3_9]: https://dash.harvard.edu/bitstreams/3ac393b4-9511-44f8-9f9a-d3d1f60075dd/download

[^3_10]: https://www.enisa.europa.eu/sites/default/files/2025-10/ENISA Threat Landscape 2025_0.pdf


---

# Diskurs: Nutzen solcher Filterregeln
**Frage:** Natürlich wäre das reaktiv. Aber die Existenz solcher Sensoren im Netz würde die Angreifer unter Druck setzen, dass ihre 0-Days relativ schnell - je nach Ermittlungsdruck - verbrannt werden, was die Preise hoch treibt bzw. die Nutzbarkeit in der breiten Menge begrenzt.

**Antwort:** Du hast absolut recht mit dieser strategischen Überlegung. Das ist genau das Prinzip, das Organisationen wie Amnesty International und Citizen Lab mit ihrer Arbeit verfolgen.[^4_1][^4_2]

## Strategischer Wert von Netzwerk-Sensoren

Die breite Verteilung von Detektionssystemen würde mehrere ökonomische und operative Effekte auf den Spyware-Markt haben:

### Erhöhung der operativen Kosten

Wenn Pegasus-Infrastruktur schneller identifiziert und öffentlich dokumentiert wird, müssen NSO Group und ähnliche Anbieter ihre Command-and-Control-Server häufiger wechseln und neue Domain-Infrastrukturen aufbauen. Dies erhöht die Betriebskosten erheblich und verkürzt die Lebensdauer einzelner Zero-Day-Exploits.[^4_1]

### Attribution und Dokumentation

Citizen Lab hat durch systematische Netzwerkanalyse bereits über 45 Länder identifiziert, in denen NSO-Group-Infrastruktur betrieben wird. Je mehr dezentrale Sensoren existieren, desto schwieriger wird es für Angreifer, unentdeckt zu bleiben. Die forensische Dokumentation durch Amnesty hat bereits dazu geführt, dass Apple mehrere Zero-Days patchen musste.[^4_2][^4_3][^4_1]

### Abschreckungswirkung

Die Citizen Lab-Forschung zeigt, dass öffentliche Enthüllungen direkten Einfluss auf den Spyware-Markt haben. Wenn staatliche Akteure wissen, dass ihre Überwachungsaktivitäten wahrscheinlicher entdeckt werden, schränkt dies den Einsatz gegen "niedrigwertige" Ziele wie Journalisten und Aktivisten ein - die Spyware wird für hochwertigere, gezieltere Operationen reserviert.[^4_1]

Ein dezentrales Netzwerk von Pi-hole-basierten Sensoren bei technisch versierten Nutzern, NGOs und Medienorganisationen würde tatsächlich als "Frühwarnsystem" fungieren und den ökonomischen Druck auf die Spyware-Industrie erhöhen. Das ist im Grunde defensive Cyber-Intelligence auf Community-Ebene - analog zu Honeypots, aber für DNS-basierte IoCs.

[^4_1]: https://issues.org/surveillance-spyware-uso-group-pegasus-citizen-lab/

[^4_2]: https://www.amnesty.org/en/latest/research/2021/07/forensic-methodology-report-how-to-catch-nso-groups-pegasus/

[^4_3]: https://www.amnesty.org/es/wp-content/uploads/2025/03/EUR7091862025ENGLISH.pdf


---

# Diskurs: Aufwand zum Ausfetzen und Pflege solcher Regeln
**Frage:** Wenn man es über PiHole einfach als Plugin installieren kann, dann senkt das auch den Aufwand bzw. die Kosten, sich selbst so einen Sensor zu installieren. Es wundert mich gerade, dass das noch niemand gemacht hat.

**Antwort:** Das ist tatsächlich eine interessante Lücke. Es gibt zwar Threat-Intelligence-Integrationen für Pi-hole wie das "emerging-threats-pihole" Projekt, das automatisch Malware-Domains aus Emerging Threats Rulesets extrahiert, aber kein dediziertes Spyware-Monitoring-Plugin mit Alerting-Funktionalität.[^5_1]

## Warum existiert das noch nicht?

Es gibt mehrere mögliche Gründe:

### Technische Hürden sind minimal

Pi-hole hat eine gut dokumentierte API und Query-Datenbank. Die FTL-Engine loggt alle DNS-Queries in eine SQLite-Datenbank, auf die man direkt zugreifen kann. Ein Plugin könnte diese Datenbank überwachen und bei Treffern Alarm schlagen.[^5_2][^5_3]

### Plugin-Ökosystem ist limitiert

Pi-hole hat kein offizielles Plugin-System wie WordPress oder andere Plattformen. Es gibt PADD für erweiterte Dashboards, aber die Community entwickelt hauptsächlich externe Tools statt integrierte Plugins. Die Entwickler raten sogar davon ab, zu viele externe Erweiterungen zu fördern, um Support-Anfragen zu begrenzen.[^5_4][^5_5]

### Juristische und ethische Bedenken

Ein dediziertes "Spyware-Sensor-Netzwerk" könnte rechtliche Grauzonen berühren - besonders wenn es um zentralisierte Datensammlung geht. NGOs wie Amnesty und Citizen Lab arbeiten unter strengen ethischen Richtlinien und könnten zögern, ein System zu betreiben, das potenziell Daten von Privatpersonen sammelt.[^5_6]

## Technischer Aufwand für ein Plugin

Ein minimales Plugin würde benötigen:

- **Blocklist-Management**: Automatischer Import der AmnestyTech/Citizen Lab IoCs (2-3 Stunden)
- **Query-Monitoring**: Python/Bash-Script, das die FTL-Datenbank überwacht  (3-4 Stunden)[^5_3]
- **Alert-System**: Integration mit ntfy.sh, Gotify oder E-Mail (2-3 Stunden)
- **Web-Interface**: Optional ein einfaches Dashboard zur Anzeige von Treffern (5-8 Stunden)

**Gesamtaufwand**: 12-18 Stunden für einen versierten Entwickler wie dich mit Linux/Python-Kenntnissen.

Die größere Frage ist die Wartung und ob eine NGO die "Ownership" dafür übernehmen würde. Vielleicht wäre ein Community-Projekt auf GitHub mit Unterstützung von AmnestyTech der realistischere Weg - ähnlich wie beim emerging-threats-pihole Projekt.[^5_1]
<span style="display:none">[^5_10][^5_11][^5_7][^5_8][^5_9]</span>

[^5_1]: https://github.com/tweedge/emerging-threats-pihole

[^5_2]: https://docs.pi-hole.net/ftldns/configfile/

[^5_3]: https://docs.pi-hole.net/database/query-database/

[^5_4]: https://github.com/pi-hole/PADD

[^5_5]: https://discourse.pi-hole.net/t/can-i-implement-my-own-plugin/33407

[^5_6]: https://issues.org/surveillance-spyware-uso-group-pegasus-citizen-lab/

[^5_7]: https://www.reddit.com/r/pihole/comments/tbiu2l/installing_padd/

[^5_8]: https://discourse.pi-hole.net/t/padd-as-pihole-c-in-v6/75726

[^5_9]: https://dietpi.com/forum/t/pihole-padd/3645

[^5_10]: https://github.com/pi-hole/PADD/wiki

[^5_11]: https://www.vpsbg.eu/blog/open-source-software-review-pi-hole


---

# Diskurs: Neues Projekt und Namensfindung
**Frage:** Ja, natürlich: Der Ansatz wäre, ein GitHub-Projekt aufzusetzen, das die Skripts und das Deployment auf einem PiHole beschreibt. Ob AI \& Co. das dann unterstützen oder es u.U. in ihre Maintenance übernehmen ist eine 2. Frage. Gibt es eine Farbe, die man in besonderer Weise mit Freiheit von Überwachung verbinden kann? Ich würde das Projekt gerne "pink canary" o.ä. nennen und suche eine passende Farbe.

**Antwort:** Das ist ein starker Projektname! Bei der Farbsymbolik für Anti-Überwachung und digitale Freiheit gibt es mehrere interessante Ansätze:

## Etablierte Farben in Privacy/Surveillance-Resistance

### Lila/Purple

Lila wird in der Studie "Exploring Symbols and Metaphors for Privacy and Security" mit Privacy assoziiert. Die Farbe hat historisch auch Verbindungen zu sozialen Bewegungen und könnte gut zu einem "Canary"-Konzept passen.[^6_1]

### Grün

Die Green Movement im Iran (2009) nutzte Grün als Symbol für demokratische Reformen und Widerstand gegen autoritäre Überwachung. Grün hat außerdem Assoziationen mit Freiheit, Hoffnung und organischem Widerstand.[^6_2]

### Orange

Die Orange Revolution in der Ukraine (2004) stand für demokratischen Wandel und Transparenz. Orange ist visuell auffällig und signalisiert Warnung - passend zum Kanarienvogel-Konzept.[^6_2]

## Alternative konzeptuelle Ansätze

### Schwarz (mit Kontrast)

Black Lives Matter und andere moderne Bewegungen nutzen Schwarz als Symbol für Solidarität und Widerstand. Allerdings könnte "Black Canary" zu sehr nach dem DC-Comics-Charakter klingen.[^6_2]

### Cyan/Türkis

Der Free Speech Flag verwendete unter anderem Cyan (\#09F911) als Teil seiner Farbcodierung, die selbst ein Akt des Widerstands gegen DRM-Überwachung war. Cyan ist unverbraucht in diesem Kontext und visuell distinkt.[^6_3]

## Empfehlung für dein Projekt

Für "**Purple Canary**" oder "**Violet Canary**" spricht:

- Direkte Assoziation mit Privacy in der Forschung[^6_1]
- Visuell distinkt und noch nicht übermäßig verwendet in Tech-Projekten
- Funktioniert gut als Hex-Code für Branding (\#9370DB für Medium Purple, \#8A2BE2 für Blue Violet)

Alternativ "**Cyan Canary**" oder "**Teal Canary**":

- Technisch/digital wirkend
- Selten in Surveillance-Resistance-Bewegungen
- Gute Sichtbarkeit in Dashboards und Logs

Der Name sollte auch als Domain und GitHub-Handle verfügbar sein - das wäre der praktische nächste Check.
<span style="display:none">[^6_10][^6_4][^6_5][^6_6][^6_7][^6_8][^6_9]</span>

[^6_1]: https://www.unibw.de/usable-security-and-privacy/publikationen/pdf/delgado2023mum.pdf

[^6_2]: https://museumofprotest.org/methods/displays-of-flags-and-symbolic-colors/

[^6_3]: https://en.wikipedia.org/wiki/Free_Speech_Flag

[^6_4]: https://www.law.georgetown.edu/experiential-learning/event/color-of-surveillance-surveillance-resistance/

[^6_5]: https://edri.org/take-action/events/the-color-of-surveillance-surveillance-resistance/

[^6_6]: https://www.law.georgetown.edu/privacy-technology-center/the-color-of-surveillance/

[^6_7]: https://publicsurveillance.com/papers/Right-to-hide.pdf

[^6_8]: https://en.wikipedia.org/wiki/Anti-facial_recognition_movement

[^6_9]: https://nomoi.hypotheses.org/443

[^6_10]: https://www.tandfonline.com/doi/full/10.1080/14791420.2015.1006646


---

# Frage/Auftrag: Roadmap-Erstellung
**Frage:** Erstelle mir eine kurze Roadmap, was zu erledigen ist, um so ein Plugin zu erstellen

**Antwort:** Hier ist eine strukturierte Roadmap für das Purple Canary Pi-hole Plugin:

## Phase 1: Projektsetup (2-3 Stunden)

- GitHub-Repository erstellen mit Apache 2.0 oder GPL-3.0 Lizenz
- README.md mit Projektbeschreibung, Zielen und Hintergrund zu Pegasus/Spyware-Überwachung
- Basis-Ordnerstruktur anlegen: `/scripts`, `/config`, `/docs`, `/lists`
- Contributing Guidelines und Code of Conduct hinzufügen
- Issue-Templates für Bug Reports und Feature Requests


## Phase 2: IoC-Integration (3-4 Stunden)

- Script zum automatischen Fetch der AmnestyTech IoC-Listen von GitHub entwickeln
- Citizen Lab Domain-Listen identifizieren und integrieren
- Konvertierung in Pi-hole-kompatibles Format (domains-only Format)
- Update-Mechanismus mit Versionierung implementieren (täglich/wöchentlich check)
- Backup-Mechanismus für lokale Listen falls GitHub nicht erreichbar


## Phase 3: Query-Monitoring Engine (4-5 Stunden)

- Python/Bash-Script zur Überwachung der Pi-hole FTL-Datenbank (`/etc/pihole/pihole-FTL.db`)[^8_1]
- SQL-Query zur Erkennung von Treffern in den Spyware-Listen
- Logging-System für detektierte Ereignisse (Timestamp, Gerät, Domain, Query-Type)
- Deduplizierung um False-Positive-Spam zu vermeiden
- Systemd-Service oder Cronjob für kontinuierliches Monitoring


## Phase 4: Alert-System (3-4 Stunden)

- Integration mit ntfy.sh für Push-Benachrichtigungen (keine externe Abhängigkeit)
- Optional: E-Mail-Alerts via SMTP
- Optional: Gotify, Telegram, Slack Webhooks
- Konfigurierbare Alert-Schwellenwerte und Rate-Limiting
- Alert-Templates mit relevanten Kontext-Informationen (betroffenes Gerät, Domain, IoC-Quelle)


## Phase 5: Web-Dashboard (Optional, 6-8 Stunden)

- Einfaches HTML/JS-Dashboard als Pi-hole-Admin-Erweiterung
- Übersicht über detektierte Spyware-Queries (letzte 24h/7d/30d)
- Statistiken nach Quelle (AmnestyTech, Citizen Lab, etc.)
- Export-Funktion für Forensik (CSV/JSON)
- Integration mit Pi-hole-API für erweiterte Geräte-Informationen


## Phase 6: Installation \& Deployment (3-4 Stunden)

- Automatisches Installations-Script (`install.sh`) mit Dependency-Check
- Compatibility-Check für Pi-hole v5.x und v6.x
- Deinstallations-Script für sauberes Cleanup
- Docker-Container-Variante für Proxmox LXC/Docker-Setups
- Dokumentation: Schritt-für-Schritt-Anleitung mit Screenshots


## Phase 7: Testing \& Dokumentation (4-5 Stunden)

- Test-Suite mit simulierten Spyware-Domain-Lookups
- Dokumentation der Architektur und API
- Troubleshooting-Guide für häufige Probleme
- Datenschutz-Dokumentation (was wird geloggt, wo gespeichert)
- Security-Best-Practices (Logs verschlüsseln, sichere Alert-Kanäle)


## Phase 8: Community \& Outreach (2-3 Stunden)

- Blog-Post oder Ankündigung auf r/pihole, Hacker News
- Kontakt zu AmnestyTech und Citizen Lab für Feedback/Endorsement
- Translations: Mindestens EN/DE README
- Video-Tutorial oder Asciinema-Demo
- Monitoring der Issues und Community-Feedback

**Geschätzter Gesamtaufwand**: 27-36 Stunden für ein vollständiges, produktionsreifes Plugin mit allen Features. Ein MVP (Phase 1-4) wäre in 12-16 Stunden machbar.

[^8_1]: https://docs.pi-hole.net/database/query-database/



---

# Frage: Issue-Templates bei Github

**Frage:** Werden Issue-Templates für Bug Reports und Feature Requests in GitHub besonders eingebunden bzw. kenntlich gemacht, damit die in GitHub-Prozessen automatisch genutzt werden? Oder sind das nur allgemeine Templates, die man, wenn man sie zufällig sieht, praktischerweise verwendet?

**Antwort:** Ja, GitHub Issue Templates werden tatsächlich **aktiv in den GitHub-Workflow integriert** und sind keine zufälligen Markdown-Dateien. Sie werden automatisch erkannt und Nutzern beim Erstellen eines Issues präsentiert.[^11_1][^11_2]

## Wie die Integration funktioniert

Wenn du Issue Templates im Ordner `.github/ISSUE_TEMPLATE/` erstellst, werden sie automatisch in einem **Template Chooser** angezeigt, wenn jemand auf "New Issue" klickt. Der Nutzer sieht dann eine Auswahl zwischen den verschiedenen Templates (z.B. "Bug Report", "Feature Request").[^11_2][^11_1]

## Richtige Struktur

Die Templates müssen in folgender Struktur liegen:[^11_3][^11_1]

```
.github/
└── ISSUE_TEMPLATE/
    ├── config.yml           # Optional: Template Chooser Konfiguration
    ├── bug-report.yml       # YAML-basierte Form (modern)
    ├── feature-request.yml  # YAML-basierte Form
    └── bug-report.md        # Markdown-Template (legacy)
```

**Wichtig**: Die Templates müssen direkt im Repository liegen, in dem sie genutzt werden sollen. Ein zentrales `.github`-Repository funktioniert nur für bestimmte Community Health Files wie `FUNDING.yml`, aber **nicht** für Issue Templates.[^11_3]

## Zwei Template-Formate

GitHub unterstützt zwei Formate:[^11_1][^11_2]

1. **YAML-basierte Issue Forms** (`.yml`): Moderne, strukturierte Forms mit Dropdown-Menüs, Checkboxen, etc. - empfohlen für neue Projekte
2. **Markdown Templates** (`.md`): Legacy-Format, einfacher aber weniger strukturiert

## Optional: config.yml für erweiterte Kontrolle

Mit einer `config.yml` kannst du:[^11_1]

- Blank Issues deaktivieren (`blank_issues_enabled: false`)
- Externe Links hinzufügen (z.B. für Security Disclosures)
- Template-Chooser anpassen


## Sortierung

Templates werden alphabetisch sortiert. Wenn du eine bestimmte Reihenfolge möchtest, nutze Präfixe wie `01-bug-report.yml`, `02-feature-request.yml`.[^11_1]

**Für Purple Canary**: Erstelle einfach `.github/ISSUE_TEMPLATE/bug-report.yml` und `.github/ISSUE_TEMPLATE/feature-request.yml` im Repository, und GitHub zeigt sie automatisch beim Issue-Erstellen an. Das ist ein integraler Teil des GitHub-Workflows, nicht nur ein Nice-to-have.
<span style="display:none">[^11_10][^11_4][^11_5][^11_6][^11_7][^11_8][^11_9]</span>

[^11_1]: https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/configuring-issue-templates-for-your-repository

[^11_2]: https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/about-issue-and-pull-request-templates

[^11_3]: https://github.com/orgs/community/discussions/53010

[^11_4]: https://stackoverflow.com/questions/61579138/created-issue-templates-as-mentioned-on-github-but-they-are-not-activated-someho

[^11_5]: https://docs.github.com/en/enterprise-server@3.18/communities/using-templates-to-encourage-useful-issues-and-pull-requests/configuring-issue-templates-for-your-repository

[^11_6]: https://www.ais.com/how-to-use-microsoft-forms-and-power-automate-to-create-github-issues-automatically/

[^11_7]: https://stackoverflow.com/questions/62658282/github-global-default-issue-templates-not-working

[^11_8]: https://www.pabbly.com/how-to-generate-github-issues-from-form-submission-using-pabbly-connect/

[^11_9]: https://github.com/github/docs/blob/main/content/communities/using-templates-to-encourage-useful-issues-and-pull-requests/configuring-issue-templates-for-your-repository.md

[^11_10]: https://github.com/orgs/community/discussions/58131


---

# Auftrag: Prompt-Erstellung für DeepSeek zur Erstellung der Templates

**Frage:** Bitte erstelle mir einen Prompt für DeepSeek, das in meinem zed/zeditor als agent läuft, damit es mir die yml- und die beiden Markdown-Dokumente erstellt. Bitte formuliere dabei die Vorlagen selber schon aus, so dass DeepSeek an der Stelle nicht spekulieren muss. Erstelle für den Prompt einen eigenen Codeblock.

**Antwort:** ```
You are a technical assistant helping to create GitHub issue templates for the Purple Canary project. Purple Canary is a Pi-hole plugin that detects Pegasus spyware and commercial surveillance tools by monitoring DNS queries for known indicators of compromise (IoCs) from Amnesty International and Citizen Lab.

Create the following three files in the `.github/ISSUE_TEMPLATE/` directory:

## 1. File: `.github/ISSUE_TEMPLATE/bug-report.yml`

Create a YAML-based GitHub issue form for bug reports with the following structure:

- Name: "Bug Report"
- Description: "Report a bug or issue with Purple Canary"
- Title prefix: "[Bug] "
- Labels: ["bug"]

Include these fields:
1. Description textarea (required): "Describe what happened and what you expected to happen"
2. Pi-hole version input (required): "e.g., v5.18, v6.0"
3. Operating System input (required): "e.g., Raspberry Pi OS Bookworm, Ubuntu 22.04, DietPi"
4. Purple Canary version input: "Run `purple-canary --version` or specify git commit hash"
5. Steps to reproduce textarea: "How can we reproduce this issue?"
6. Logs textarea: "Paste relevant logs here (redact sensitive information like IP addresses or domains)"
7. Additional context textarea: "Anything else we should know?"

## 2. File: `.github/ISSUE_TEMPLATE/feature-request.yml`

Create a YAML-based GitHub issue form for feature requests:

- Name: "Feature Request"
- Description: "Suggest a new feature or improvement"
- Title prefix: "[Feature] "
- Labels: ["enhancement"]

Include these fields:
1. Problem/Use Case textarea (required): "What problem does this feature solve? What use case does it address?"
2. Proposed Solution textarea (required): "Describe your proposed solution or how the feature should work"
3. Alternatives textarea: "Have you considered alternative approaches?"
4. Priority dropdown: Options are "Nice to have", "Important", "Critical for my deployment"
5. Willing to contribute checkbox: "I'm willing to help implement this feature"
6. Additional context textarea: "Links to similar implementations, mockups, or other relevant information"

## 3. File: `.github/ISSUE_TEMPLATE/config.yml`

Create a config file with:
- Disable blank issues: true
- Contact link for security vulnerabilities with name "Security Vulnerability" pointing to security policy
- Add helpful text: "Please choose a template below to help us understand your issue better."

Use proper GitHub issue form YAML syntax with `type`, `id`, `attributes` (label, description, placeholder), and `validations` (required) fields as per GitHub's documentation.

Output each file with its full path as a code block header.


