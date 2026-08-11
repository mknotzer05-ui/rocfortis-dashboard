# RocFortis Signal

SEO- und GEO-Lagebild der RocFortis Group. Eine HTML-Datei, keine Abhängigkeiten,
läuft auch offline.

**Live:** https://mknotzer05-ui.github.io/rocfortis-dashboard/

Zugangsdaten werden separat übergeben.

---

## Was das Dashboard zeigt

| Kanal | Bedeutung | Kernfrage |
|---|---|---|
| **SEO** | Search Engine Optimization | Wo steht RocFortis in klassischen Suchergebnissen? |
| **GEO** | Generative Engine Optimization | Wird RocFortis in KI-Antworten zitiert? |

Sechs Kennzahlen, Sichtbarkeit über zwölf Monate, Zitationsanteil je KI-Engine,
Keyword-Lage, Märkte und Regionen, Prompt-Monitor und die technische Basis.

## Vier Designvarianten

Oben rechts umschaltbar, die Auswahl bleibt gespeichert. Alle vier tauschen nur
Farb- und Formtokens, nie die Struktur.

- **Dossier** — dunkel, Mitternachtsblau mit Messing
- **Cupertino** — hell, Apple-Karten auf kühlem Grau
- **Gunmetal** — dunkel monochrom, kantig, Monospace-Titel
- **Vellum** — helles Papier, Tintenblau und Stempelrot, für Ausdruck und PDF

## Daten

Alle Zahlen sind **Demodaten** und in der Kopfzeile als solche markiert. Sie liegen
gesammelt im Objekt `DATA` am Anfang des `<script>`-Blocks in `index.html`. Für
echte Zahlen wird ausschließlich dieses Objekt ersetzt — Layout, Diagramme und
Tabellen leiten sich vollständig daraus ab.

Anzubindende Quellen: Google Search Console und Sistrix oder Ahrefs für SEO, GA4
für Sitzungen, ein GEO-Monitoring für den Prompt-Monitor.

## Sicherheit

Die Passwortabfrage ist eine **clientseitige Sperre**. Sie hält Gelegenheitszugriffe
ab, ersetzt aber keine Zugriffskontrolle: Der Seitenquelltext ist einsehbar, und der
hinterlegte SHA-256-Hash lässt sich offline durchprobieren. Deshalb enthält diese
Seite ausschließlich Demodaten.

Vor dem Einsatz mit echten Kundenzahlen braucht es serverseitige Authentifizierung —
etwa Cloudflare Access vor der Seite oder Auslieferung über einen Server mit
Session-Cookie und Passwort-Hash (Argon2id) in der Datenbank.

Details zu Farbpalette, Typografie, Layout und offenen Punkten stehen in
[Plan.md](Plan.md).
