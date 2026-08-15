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

Sechs Kennzahlen, der Seitenbestand über zwölf Monate, die Bereitschaft je
KI-Engine, die Keyword-Lage, der Seitenbestand nach Seitentyp, der Prompt-Monitor
und die technische Basis.

## Zwei Ansichten

Im Kopf umschaltbar, die Auswahl bleibt gespeichert. Beide tauschen nur Farb-
und Formtokens, nie die Struktur.

- **Bildschirm:** die Hausidentität von rocfortis.com. Kohle `#1C1C1C` gegen
  Off-White `#E6E6E6`, Feldkhaki als einziger Akzent, Radius 0, Versal-Titel
  in Work Sans. Dieselben Farbwerte wie die Unternehmensseite.
- **Papier:** heller Untergrund mit Tintenblau, für Ausdruck und PDF.

Drei frühere Entwürfe (Dossier, Cupertino, Gunmetal) liegen weiter als Tokens
im Stylesheet, werden aber nicht mehr angeboten. Wer sie sehen will, setzt
`data-variant` am `<html>`-Element von Hand.

Beim Drucken wird die Papier-Palette unabhängig von der gewählten Ansicht
erzwungen. Bedienelemente entfallen, Kacheln und Tabellen brechen nicht mitten
durch, der Maßnahmenplan beginnt auf einer eigenen Seite.

## Schrift

Work Sans, dieselbe Schrift wie auf rocfortis.com. Sie liegt als Variable Font
base64-kodiert in `index.html`. Damit sieht das Dashboard auch ohne Netzverbindung
so aus wie die Website.

## Daten

Alle Zahlen stammen aus einer eigenen Erhebung vom **12. August 2026**: Vollcrawl
aller 98 Sitemap-URLs von rocfortis.com, Auswertung der ausgelieferten
HTML-Dokumente, Browser-Messung der Ladezeiten und sechs echte Suchabfragen.
Nichts ist geschätzt.

Die vollständigen Befunde mit Maßnahmenplan stehen in [AUDIT.md](AUDIT.md).
Kurzfassung: SEO 54/100, GEO 55/100. Drei kritische Punkte: auf allen 98 Seiten
fehlt `hreflang`, die fünf Leistungsseiten haben keine H1, und 457 von 476 Bildern
haben keinen Alt-Text.

Die Werte liegen gesammelt im Objekt `DATA` am Anfang des `<script>`-Blocks in
`index.html`. Bei jeder Neuerhebung wird nur dieses Objekt ersetzt.

Noch nicht erhoben, weil dafür Zugänge fehlen: Besucherzahlen und Klicks (Search
Console, GA4), Keyword-Positionen (Sistrix oder Ahrefs), Feldwerte für
Core Web Vitals und echte Zitationen in ChatGPT oder Perplexity.

Welche Zugänge und Angaben für den Start der Optimierung nötig sind, steht
gesammelt in [ANFORDERUNGEN.md](ANFORDERUNGEN.md). Wie die Seite abgesichert
wird, sobald echte Zahlen darin stehen, steht in [ABSICHERUNG.md](ABSICHERUNG.md).

Als Beigabe liegt ein fertiger Entwurf für [llms.txt](llms.txt) bei. Alle 43
verlinkten Seiten wurden auf Erreichbarkeit geprüft.

## Sicherheit

Die Passwortabfrage ist eine **clientseitige Sperre**. Sie hält Gelegenheitszugriffe
ab, ersetzt aber keine Zugriffskontrolle: Der Seitenquelltext ist einsehbar, und der
hinterlegte SHA-256-Hash lässt sich offline durchprobieren.

Die enthaltenen Daten stammen ausschließlich aus öffentlich abrufbaren Quellen:
der Website selbst und den Suchergebnissen. Es sind keine vertraulichen Kundendaten
darin. Wer das Repository liest, sieht allerdings die Bewertung der Website;
solange das Repository öffentlich ist, gilt das für jeden.

Vor dem Einsatz mit echten Kundenzahlen braucht es serverseitige Authentifizierung,
etwa Cloudflare Access vor der Seite oder Auslieferung über einen Server mit
Session-Cookie und Passwort-Hash (Argon2id) in der Datenbank.

Details zu Farbpalette, Typografie, Layout und offenen Punkten stehen in
[Plan.md](Plan.md).
