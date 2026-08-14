# RocFortis Signal: SEO- und GEO-Dashboard

**Projekt:** Internes Performance-Dashboard für die RocFortis Group
**Stand:** 12. August 2026 · erste Erhebung eingearbeitet
**Datei:** `index.html` (eine Datei, keine Abhängigkeiten, offline lauffähig)

---

## 1. Was das Dashboard ist

Ein passwortgeschütztes Lagebild für zwei Sichtbarkeitskanäle:

| Kanal | Bedeutung | Kernfrage |
|---|---|---|
| **SEO** | Search Engine Optimization | Wo steht RocFortis in klassischen Suchergebnissen? |
| **GEO** | Generative Engine Optimization | Wird RocFortis in KI-Antworten (ChatGPT, Perplexity, Google AI Overviews, Claude, Copilot) zitiert? |

> **Annahme:** „GEO" ist als *Generative Engine Optimization* umgesetzt, das übliche Gegenstück zu SEO. Falls die geografische Lesart gemeint war, wird aus dem Sichtbarkeitstest ein Standort-Ranking; dafür braucht es GA4-Zugang.

Die Befunde der ersten Erhebung stehen in [AUDIT.md](AUDIT.md).

---

## 2. Gestaltungsthese

Zwei Anforderungen, die sich normalerweise widersprechen:

- **Apple-minimalistisch:** ruhige Flächen, präzise Typo-Hierarchie, keine Dekoration.
- **Geheimagent, aber seriös:** kein Matrix-Grün, kein Gamer-Neon.

Die Auflösung: **das Dossier**, nicht der Hacker-Terminal. Die Bildsprache kommt vom Lagebericht eines Nachrichtendienstes: Klassifizierungsleisten, Freigabestufe, Zeitstempel in Zulu-Zeit, Messing statt Neon, Mitternachtsblau statt Schwarz. Bond trägt Smoking, nicht Kapuzenpulli.

**Der ganze Mut steckt an einer Stelle:** im Zugangsbildschirm. Eine Iris-Blende, die sich beim Freischalten öffnet. Danach wird die Oberfläche still und arbeitet.

---

## 3. Farbpalette

### Variante A: `DOSSIER` (Standard, dunkel)
Mitternachtsblau mit Messing. Die Signatur der Marke.

| Token | Hex | Einsatz |
|---|---|---|
| `--ground` | `#0A1017` | Seitengrund, blaustichiges Fast-Schwarz |
| `--surface` | `#101A24` | Panels |
| `--line` | `#1E2B38` | Haarlinien, Panelrahmen |
| `--ink` | `#E8EEF4` | Primärtext |
| `--ink-2` | `#8A9DAF` | Sekundärtext, Achsen |
| `--accent` | `#D3A84C` | Messing für Marke, aktiven Zustand und Chart-Endpunkt |
| `--pos` | `#4FA88B` | positive Entwicklung (gedämpftes Petrolgrün) |
| `--neg` | `#DB7C72` | Mangel, negativer Befund |

### Variante B: `CUPERTINO` (hell, Apple)
Kühles Weiß, Frostglas, dieselbe Messing-Marke in dunklerer Sättigung.

| Token | Hex |
|---|---|
| `--ground` | `#F5F7F9` |
| `--surface` | `#FFFFFF` |
| `--line` | `#E1E7EC` |
| `--ink` | `#0B1219` |
| `--ink-2` | `#5C6C7B` |
| `--accent` | `#8A6714` |
| `--pos` / `--neg` | `#2E7D63` / `#B23A31` |

### Variante C: `GUNMETAL` (dunkel, monochrom)
Neutraler Waffenstahl, Radius 0, dichter gesetzt, Titel in Monospace. Instrumententafel statt Dokument.

| Token | Hex |
|---|---|
| `--ground` | `#0D0F10` |
| `--surface` | `#15181A` |
| `--line` | `#282D30` |
| `--ink` | `#EDEFF0` |
| `--ink-2` | `#8B9296` |
| `--accent` | `#DDE2E5` (das Licht selbst ist der Akzent) |
| `--pos` / `--neg` | `#7FA98C` / `#D07B70` |

### Variante D: `VELLUM` (hell, freigegebenes Dokument)
Kühles Papier mit Tintenblau und Stempelrot. Für Ausdruck und PDF-Export.

| Token | Hex |
|---|---|
| `--ground` | `#EEF0EC` |
| `--surface` | `#F8F9F6` |
| `--line` | `#D6DAD3` |
| `--ink` | `#141C22` |
| `--ink-2` | `#5E6B6E` |
| `--accent` | `#1F4E6B` |
| `--pos` / `--neg` | `#2F6B4F` / `#9E3B2E` |

**Semantik ist vom Akzent getrennt.** Grün/Gelb/Rot bedeuten immer nur Bewertung, nie Marke. Kein Wert wird ausschließlich über Farbe kodiert: jede Bewertung trägt zusätzlich ihre Zahl, jede Alarm-Kachel eine linke Kante. Alle vier Varianten wurden gemessen: schlechtester Textkontrast 4,67:1.

---

## 4. Typografie

Die Schrift kommt von der Website. rocfortis.com setzt Überschriften und Fließtext in **Work Sans**, das Dashboard tut dasselbe. Es soll neben der Website nicht wie ein fremdes Werkzeug aussehen.

Work Sans liegt als Variable Font base64-kodiert in `index.html`: latin-Schnitt, rund 50 KB, alle Gewichte von 300 bis 700 aus einer Datei. Keine Webfont-URL, keine CDN-Abhängigkeit. Die Datei bleibt offline lauffähig, und es gibt keinen stillen Fallback auf eine andere Schrift.

| Rolle | Schrift | Einsatz |
|---|---|---|
| **Display** | Work Sans 600 | Wortmarke, Panel-Titel, KPI-Zahlen |
| **UI / Fließtext** | Work Sans 400 | Tabellen, Beschreibungen, Buttons |
| **Utility** | `SF Mono → Menlo → monospace` | Klassifizierungscodes, Zeitstempel, Achsen, Positionen |

Display-Elemente tragen 600, weil Work Sans in Versalien mit Laufweite bei 500 zu dünn wird. Die Monospace bleibt Systemschrift; sie trägt keine Markenbedeutung, sondern hält Zeitstempel und Zahlenspalten auf gleicher Breite. In `GUNMETAL` übernimmt sie zusätzlich die Display-Rolle.

Der eingebettete Schnitt deckt Latin ab. Die wenigen Zeichen außerhalb davon (`Δ` in der Keyword-Tabelle, `◆` in der Klassifizierungsleiste) kommen aus der Systemschrift.

**Skala** (1.25 Major Third): 11 · 12 · 13 · 15 · 19 · 24 · 34 px
**Regeln:** Versal-Labels mit `0.14em` Laufweite · alle Zahlenspalten `tabular-nums` · Überschriften `text-wrap: balance`

---

## 5. Layout

Ein Raster, vier Varianten. Die Varianten tauschen ausschließlich Tokens (Farbe, Radius, Schrift, Körnung), nie die Struktur. Deshalb bleibt jede Variante wartbar.

```
┌──────────────────────────────────────────────────────────────┐
│ VERTRAULICH · FREIGABESTUFE 2 · 2026-08-12 16:38Z    [Design▾]│  Klassifizierungsleiste
├──────────────────────────────────────────────────────────────┤
│ ROCFORTIS SIGNAL      Vollcrawl 98 Seiten          [Abmelden] │  Kopf
├──────────────────────────────────────────────────────────────┤
│ ┌──────┐┌──────┐┌──────┐ ┌──────┐┌──────┐┌──────┐            │
│ │ SEO  ││ SEO  ││ SEO  │ │ GEO  ││ GEO  ││ GEO  │            │  6 Kennzahl-Kacheln
│ └──────┘└──────┘└──────┘ └──────┘└──────┘└──────┘            │  links SEO, rechts GEO
├───────────────────────────────────┬──────────────────────────┤
│ Seitenbestand über Zeit           │ KI-Engines               │
│ (zwei Reihen, Doppelachse:        │ (Bereitschaft je Engine, │
│  Seiten gesamt / Anteil EN)       │  Balken + Schwerpunkt)   │
├───────────────────────────────────┼──────────────────────────┤
│ Keyword-Lage (Tabelle)            │ Seitenbestand            │
├───────────────────────────────────┴──────────────────────────┤
│ PROMPT-MONITOR: echte Suchanfragen, gefunden ja/nein          │  Signatur-Modul
├──────────────────────────────────────────────────────────────┤
│ Technische Basis: Serverantwort · Ladezeit · CSS · Codes      │
└──────────────────────────────────────────────────────────────┘

Das Raster ist unverändert das der ersten Fassung. Nur zwei Panel-Titel wurden
angepasst, weil der alte Titel mit den erhobenen Daten eine Falschaussage wäre:
aus „Sichtbarkeit über Zeit" wurde „Seitenbestand über Zeit", aus „Märkte &
Regionen" wurde „Seitenbestand". Beide zeigen echte Messwerte.
```

**Links SEO, rechts GEO.** Die Trennung ist über die gesamte Seite konstant, damit der Blick sie nach dem ersten Scan nicht mehr suchen muss.

**Breakpoints:** 375 · 768 · 1024 · 1440 px. Tabellen scrollen in eigenem Container, der Seitenkörper nie horizontal.

---

## 6. Signatur-Elemente

1. **Die Iris.** Der Zugangsbildschirm öffnet sich beim Freischalten wie eine Blende. Eine einzige inszenierte Bewegung, danach Ruhe. Bei `prefers-reduced-motion` blendet sie ohne Rotation über.
2. **Der Prompt-Monitor.** Das Modul, das es auf keinem SEO-Dashboard gibt: echte Suchanfragen, ob rocfortis.com in den Ergebnissen steht und welcher Wettbewerber stattdessen. Das ist der eigentliche GEO-Wert und passt exakt zum Überwachungs-Motiv.

   **Keine Angabe ist keine Null.** Wo ein Wert nicht erhoben werden konnte, steht „k. A." statt einer Schätzung. Betroffen sind die Spalten Δ und Volumen in der Keyword-Lage; beide brauchen Search-Console-Zugang. Die Zeitreihe im Diagramm stammt aus den Änderungsdaten der Sitemap, der einzigen Historie, die ohne fremde Zugänge messbar ist.
3. **Die Klassifizierungsleiste.** Freigabestufe und laufender Zulu-Zeitstempel. Trägt echte Information (Sitzungskontext), ist keine Dekoration.

---

## 7. Zugang

- **Benutzer:** `rocfortis`
- **Passwort:** wird separat übergeben und steht bewusst **nicht** in diesem Repository (siehe `ZUGANG.txt`, lokal und nicht versioniert).
- Der Nutzer wird einmalig angelegt. Es gibt bewusst keine Oberfläche für Selbstverwaltung, Passwortänderung oder Registrierung.
- Sitzung hält über `sessionStorage`; Schließen des Tabs meldet ab.
- Fünf Fehlversuche sperren die Eingabe für 60 Sekunden.
- Hinterlegt ist ein **SHA-256-Hash** (`c5a04f…654f`) über `benutzer:passwort:salt`, kein Klartext.

### Sicherheitseinstufung, bitte lesen

Das ist eine **clientseitige Zugangssperre**. Sie hält Gelegenheitszugriffe ab, ist aber keine echte Zugriffskontrolle: Wer die Seitenquelle öffnet, sieht den Hash und die Daten. Für die aktuelle Nutzung (Demodaten, interne Ansicht) ist das angemessen.

Solange die Seite über GitHub Pages aus einem **öffentlichen** Repository ausgeliefert wird, gilt zusätzlich: Die Seite ist für jeden erreichbar, der die URL kennt, und der Hash lässt sich offline auf das Passwort hin durchprobieren. Das Passwort ist damit eine Höflichkeitsbarriere, kein Schutz. Deshalb enthält die Seite ausschließlich Demodaten.

Sobald echte Kundenzahlen darin stehen, braucht es serverseitige Authentifizierung. Konkret:

1. Statisches Hosting hinter Basic Auth oder Cloudflare Access, **oder**
2. Auslieferung über einen kleinen Server mit Session-Cookie und Passwort-Hash in der Datenbank (Argon2id), Daten erst nach erfolgreichem Login per API.

Ich setze das um, sobald das gewünscht ist.

---

## 8. Daten

Alle Zahlen stammen aus einer **eigenen Erhebung am 12. August 2026**: Vollcrawl aller 98 Sitemap-URLs von rocfortis.com, Auswertung der ausgelieferten HTML-Dokumente, Browser-Messung der Ladezeiten und sechs echte Suchabfragen. Nichts ist geschätzt oder erfunden.

Sie liegen gesammelt in einem einzigen Objekt am Anfang des `<script>`-Blocks:

```js
const DATA = {
  kpis:       [...],  // 6 Kennzahlen-Kacheln
  categories: [...],  // 7 SEO-Kategorien mit Gewicht
  geodims:    [...],  // 4 GEO-Dimensionen
  findings:   [...],  // Befunde nach Schwere
  bestand:    [...],  // Seitenbestand aus der Sitemap
  prompts:    [...],  // Sichtbarkeitstest
  vitals:     [...]   // technische Messwerte
};
```

Bei jeder Neuerhebung wird nur dieses Objekt ersetzt. Layout, Balken und Tabellen leiten sich vollständig daraus ab.

### Was gemessen wurde und was noch fehlt

| Erhoben | Wie |
|---|---|
| Statuscodes, Titel, Beschreibungen, H1, Canonical, hreflang | Vollcrawl der 98 Sitemap-URLs |
| Schema.org, Bilder, Alt-Texte, interne Verlinkung, Textlänge | Auswertung der ausgelieferten HTML-Dokumente |
| Serverantwort, Ladezeit, Ressourcengewicht | Browser-Messung (Navigation Timing) |
| Auffindbarkeit bei sechs Suchanfragen | echte Abfragen am 12. August 2026 |

| Noch nicht erhoben | Wird gebraucht |
|---|---|
| Besucherzahlen, Klicks, Impressionen | Zugang zu Google Search Console und GA4 |
| Keyword-Positionen und Suchvolumen | Search Console oder Sistrix/Ahrefs |
| LCP, INP, CLS aus echten Nutzersitzungen | CrUX-Feldwerte über die Search Console |
| Zitationen in ChatGPT, Perplexity, Claude | GEO-Monitoring (Peec AI, Otterly) oder eigenes Prompt-Sampling |
| Entwicklung über Zeit | zweite Erhebung, diese hier ist der Nullpunkt |

---

## 9. Qualitätsanforderungen

- [x] Kontrast ≥ 4.5:1 für Fließtext in allen vier Varianten
- [x] Tastaturbedienbar, Fokus überall sichtbar
- [x] `prefers-reduced-motion` respektiert
- [x] Keine Emoji als Icons, stattdessen Inline-SVG
- [x] Übergänge 150 bis 300 ms
- [x] Responsiv ab 375 px, kein horizontales Scrollen des Seitenkörpers
- [x] Läuft ohne Netzwerkzugriff (keine CDN-Abhängigkeit)

---

## 10. Offene Punkte

| # | Punkt | Entscheidung durch |
|---|---|---|
| 1 | GEO = Generative *oder* geografisch? Aktuell beides, Schwerpunkt generativ. | RocFortis |
| 2 | Branche der Demodaten ist als Sicherheits- und Infrastrukturdienstleistung angenommen, echte Keywords ersetzen. | RocFortis |
| 3 | Echte Datenanbindung (Search Console / GA4 / GEO-Monitoring) | nach Freigabe |
| 4 | Serverseitige Authentifizierung vor Einsatz mit echten Zahlen | vor Produktivbetrieb |
| 5 | Eigene Domain statt Artifact-URL | RocFortis |
