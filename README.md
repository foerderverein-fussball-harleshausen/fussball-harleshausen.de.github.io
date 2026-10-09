# Förderverein Fußball der SVH Kassel – Website

Statische Website mit [Hugo](https://gohugo.io) und dem Theme [Ananke](https://themes.gohugo.io/themes/gohugo-theme-ananke/) (als Git-Submodul in `themes/ananke`).
Design und Farben sind an [svhkassel-fussball.de](https://www.svhkassel-fussball.de/) und den Entwurf in `docs/` angelehnt.

## Lokal starten

```bash
git submodule update --init --recursive   # nur beim ersten Mal
hugo server
```

Dann <http://localhost:1313> öffnen. Für die fertige Seite: `hugo --gc --minify` (Ausgabe in `public/`).

## Wo pflege ich was?

| Was | Datei |
| --- | --- |
| Kontaktdaten, Bankverbindung, Beiträge, Formular-Endpunkt | `hugo.toml` → `[params]` |
| Menü | `hugo.toml` → `[menus]` |
| Kennzahlen & Wirkung auf der Startseite | `data/startseite.yaml` |
| Vorstand | `data/vorstand.yaml` (Fotos nach `static/images/vorstand/`) |
| Sponsoring-Pakete Bronze/Silber/Gold | `data/sponsoring.yaml` |
| Seiten (Über uns, Mitglied werden, …) | `content/*.md` |
| Förderprojekte | `content/projekte/*.md` |
| Farben & Layout | `assets/ananke/css/fv.css` |

### Neues Förderprojekt anlegen

```bash
hugo new content projekte/neues-projekt.md
```

Im Front Matter `status` auf `geplant`, `umsetzung` oder `abgeschlossen` setzen und optional ein Bild (`image: images/projekte/...jpg`) angeben.

### Bilder

Echte Fotos einfach unter `static/images/` ablegen und per Front Matter einbinden:
`heroImage: images/mein-bild.jpg` (Kopfbereich jeder Seite) oder `image:` (Projekte).

### Shortcodes für Inhalte

`{{< raster spalten="3" >}}`, `{{< karte icon="euro" titel="…" >}}`, `{{< box titel="…" >}}`, `{{< button url="/kontakt/" >}}`,
`{{< faq >}}{{< frage "…?" >}}…{{< /frage >}}{{< /faq >}}`, `{{< vorstand >}}`, `{{< sponsorpakete >}}`,
`{{< mitgliedsantrag >}}`, `{{< sponsoranfrage >}}`, `{{< kontaktformular >}}`.

## Formulare

GitHub Pages kann keine Formulare verarbeiten. Solange `formEndpoint` in `hugo.toml` leer ist, öffnen die Formulare das E-Mail-Programm des Besuchers (`mailto:`).
Empfohlen: einen Formulardienst (z. B. Formspree, Getform) einrichten und dessen URL als `formEndpoint` eintragen. Den Dienst dann in der Datenschutzerklärung ergänzen.

Optional: Liegt eine Datei `static/downloads/mitgliedsantrag.pdf` vor, erscheint automatisch ein Button „Antrag als PDF“.

## Veröffentlichen

`.github/workflows/hugo.yml` baut und veröffentlicht die Seite bei jedem Push auf `main` über GitHub Pages.
In den Repository-Einstellungen unter *Settings → Pages* als Quelle **GitHub Actions** wählen. Die Domain steht in `static/CNAME`.

## Vor dem Livegang

- [ ] Platzhalter in `hugo.toml` (Adresse, E-Mail, IBAN) ersetzen
- [ ] Vorstand in `data/vorstand.yaml` eintragen
- [ ] Impressum und Datenschutz vervollständigen (`[ … ]`-Stellen)
- [ ] Kennzahlen und Projekte aktualisieren
- [ ] Formular-Endpunkt einrichten
- [ ] Logo durch das offizielle Vereinslogo ersetzen (`static/images/logo.svg`)
