# Aurion Systems — Website

Landingpage von Aurion Systems (Einzelunternehmen Marcel Nika, Wien):
KI-Automatisierung für KMU in Wien und dem DACH-Raum (Chatbots, Terminbuchung,
Workflows). Sprache der Seite: Deutsch (Österreich), Anrede "Sie".

## Aufbau
- Statische Seite, **kein Build**. Alles in `index.html` (HTML + CSS + JS inline).
- Weitere Dateien: `CNAME`, `robots.txt`, `sitemap.xml`, Logo/Favicons (PNG).
- Impressum, Datenschutzerklärung, Cookie-Banner und Branchen-Modals stehen
  als Overlays in `index.html`.

## Hosting und Deployment
- GitHub Pages, ausgeliefert wird `main`. Deploy = Push/Merge nach `main`.
- Domain `aurion-systems.at` (Datei `CNAME`), gekauft und DNS bei Hosttech.
- Arbeitsbranches nie direkt live: erst nach `main` mergen.

## Chat und Formulare (Backend nicht in diesem Repo)
- Chat-Widget "Lisa": sendet den Verlauf per POST an `CHAT_PROXY`
  (n8n-Webhook `/webhook/aurion-chat`), Antwort steht in `data.text`.
- Terminflow: Enthält die Antwort "alles klar, ich nehme das kurz auf", fragt
  der Browser Name und Telefon ab und sendet sie an `NOTIFY_PROXY`
  (`/webhook/aurion-notify`, vermutlich Telegram-Benachrichtigung).
- **Stand:** n8n läuft lokal auf Marcels Mac und wird per ngrok erreicht.
  Geplant: Umzug auf einen Hetzner-Server, dann `https://webhook.aurion-systems.at`.
  Dann `CHAT_PROXY`/`NOTIFY_PROXY` in `index.html` ändern und die
  Datenschutzerklärung anpassen (ngrok raus, Hetzner rein).
- Kontaktformular (3 Schritte): geht per `formsubmit.co` an
  `office@aurion-systems.at`, nicht über n8n.

## Regeln
- Keine Geheimnisse (Tokens, Passwörter, API-Schlüssel) ins Repo.
- Keine erfundenen Kundenstimmen, Bewertungen oder Zahlen. Beispielwerte in
  Mockups müssen als Beispiel erkennbar sein.
- Keine Preisangaben auf der Website.
- Jeder neue Drittanbieter (Hosting, Fonts, Skripte, Formulare, Chat-Backend)
  muss in der Datenschutzerklärung stehen. Keine Tracking-/Analyse-Tools ohne
  Einwilligungsbanner.
- Cookie-Banner: Das Lesen der Datenschutzerklärung darf nie als Zustimmung
  gelten.
- Formularfelder immer mit `<label for>` und `id`.

## Prüfen vor dem Push
- JS-Syntax: Skript aus `index.html` extrahieren und `node --check` ausführen.
- Lokal ansehen: `python3 -m http.server 8080` und mit Playwright/Chromium
  (`/opt/pw-browsers`) einen Screenshot machen. Externe Skripte (three.js,
  Chat-Backend) laden in der Sandbox nicht, das ist kein Fehler.

## Bekannte offene Punkte
- Datenschutzerklärung nennt weder ngrok noch den Cloudflare-CDN (three.js
  wird zur Laufzeit von cdnjs.cloudflare.com geladen).
- Branch `claude/chat-zugriff-7dgjr3` ist nicht in `main` gemerged; `main` hat
  parallel ähnliche Änderungen (Favicon, robots, sitemap). Vor dem Merge
  abgleichen. Nur auf dem Branch: Cookie-Banner-Fix, Label-Verknüpfung,
  Datenschutzhinweis am Formular, Cookie-Einstellungen im Footer, JSON-LD.
- Keine echten Kundenstimmen/Referenzen auf der Seite (erst mit echten Kunden).
- Server-Infrastruktur und Betriebsdokumentation liegen im privaten Repo
  `aurion-infra` (geplant).
