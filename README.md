# BPMNDesk

BPMNDesk ist ein kostenloser, deutschsprachiger BPMN-2.0-Editor im Browser und Teil der DESK Suite von Wissen & Werkzeug. Das Tool läuft vollständig clientseitig: Diagramme werden lokal im Browser geöffnet, bearbeitet und wieder heruntergeladen. Es gibt kein Backend, keine Anmeldung und keine serverseitige Speicherung von Diagrammen.

## Tech-Stack

- Statische Website mit HTML, CSS und Vanilla JavaScript
- `bpmn-js` 18.14.0 als lokal eingebundener Vendor-Baustein
- `nginx:alpine` im Docker-Container
- Deployment per Docker auf Coolify

## Lokal testen

```bash
docker build -t bpmndesk . && docker run -p 8080:80 bpmndesk
```

Danach ist die Anwendung unter `http://localhost:8080` erreichbar.

## Deployment in Coolify

Repository in Coolify verbinden, den Dockerfile-Build-Pack verwenden, die Domain `bpmn.wissen-und-werkzeug.de` setzen und deployen.

## Suchmaschinen

- `public/robots.txt` erlaubt allen Crawlern alles und verweist auf die Sitemap.
- `public/sitemap.xml` führt die Startseite `https://bpmn.wissen-und-werkzeug.de/`. Bei inhaltlichen Änderungen an `index.html` das Datum in `lastmod` nachziehen.
- nginx liefert nur vorhandene Dateien aus. Unbekannte Adressen bekommen Status 404 mit dem Inhalt von `public/404.html` (`noindex`).
- `/index.html` leitet per 301 auf `/` um, `/impressum.html` per 301 auf `https://wissen-und-werkzeug.de/impressum/`.
- `index.html` enthält Canonical, JSON-LD (`WebApplication`) und `og:image` (`public/assets/images/og-bpmndesk.png`, 1200 x 630).
- Die Sicherheits-Header stehen in `security-headers.conf` und werden in jeder `location` mit eigenem `add_header` eingebunden, weil nginx sie sonst dort nicht vererbt.

## Hinweis zu Inter

Die Inter-Fontdateien müssen manuell in `public/assets/fonts/` hinterlegt werden. Quelle: https://rsms.me/inter/

## Lizenz

Dieses Projekt steht unter der MIT-Lizenz. `bpmn-js` steht unter der Lizenz von bpmn.io: https://bpmn.io/license/
