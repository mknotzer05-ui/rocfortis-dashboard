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

Alle Zahlen stammen aus einer eigenen Erhebung vom **12. August 2026**: Vollcrawl
aller 98 Sitemap-URLs von rocfortis.com, Auswertung der ausgelieferten
HTML-Dokumente, Browser-Messung der Ladezeiten und sechs echte Suchabfragen.
Nichts ist geschätzt.

Die vollständigen Befunde mit Maßnahmenplan stehen in [AUDIT.md](AUDIT.md).
Kurzfassung: SEO 54/100, GEO 55/100. Drei kritische Punkte — auf allen 98 Seiten
fehlt `hreflang`, die fünf Leistungsseiten haben keine H1, und 457 von 476 Bildern
haben keinen Alt-Text.

Die Werte liegen gesammelt im Objekt `DATA` am Anfang des `<script>`-Blocks in
`index.html`. Bei jeder Neuerhebung wird nur dieses Objekt ersetzt.

Noch nicht erhoben, weil dafür Zugänge fehlen: Besucherzahlen und Klicks (Search
Console, GA4), Keyword-Positionen (Sistrix oder Ahrefs), Feldwerte für
Core Web Vitals und echte Zitationen in ChatGPT oder Perplexity.

Als Beigabe liegt ein fertiger Entwurf für [llms.txt](llms.txt) bei — alle 43
verlinkten Seiten wurden auf Erreichbarkeit geprüft.

## Sicherheit

Die Passwortabfrage ist eine **clientseitige Sperre**. Sie hält Gelegenheitszugriffe
ab, ersetzt aber keine Zugriffskontrolle: Der Seitenquelltext ist einsehbar, und der
hinterlegte SHA-256-Hash lässt sich offline durchprobieren.

Die enthaltenen Daten stammen ausschließlich aus öffentlich abrufbaren Quellen —
der Website selbst und Suchergebnissen. Es sind keine vertraulichen Kundendaten
darin. Wer das Repository liest, sieht allerdings die Bewertung der Website;
solange das Repository öffentlich ist, gilt das für jeden.

Vor dem Einsatz mit echten Kundenzahlen braucht es serverseitige Authentifizierung —
etwa Cloudflare Access vor der Seite oder Auslieferung über einen Server mit
Session-Cookie und Passwort-Hash (Argon2id) in der Datenbank.

Details zu Farbpalette, Typografie, Layout und offenen Punkten stehen in
[Plan.md](Plan.md).
