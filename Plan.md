# RocFortis Signal — SEO- & GEO-Dashboard

**Projekt:** Internes Performance-Dashboard für die RocFortis Group
**Stand:** 10. August 2026
**Datei:** `index.html` (eine Datei, keine Abhängigkeiten, offline lauffähig)

---

## 1. Was das Dashboard ist

Ein passwortgeschütztes Lagebild für zwei Sichtbarkeitskanäle:

| Kanal | Bedeutung | Kernfrage |
|---|---|---|
| **SEO** | Search Engine Optimization | Wo steht RocFortis in klassischen Suchergebnissen? |
| **GEO** | Generative Engine Optimization | Wird RocFortis in KI-Antworten (ChatGPT, Perplexity, Google AI Overviews, Claude, Copilot) zitiert? |

> **Annahme:** „GEO" ist hier als *Generative Engine Optimization* umgesetzt — das übliche Gegenstück zu SEO. Die geografische Lesart ist trotzdem abgedeckt: das Panel **Märkte & Regionen** zeigt die Verteilung nach Bundesland und DACH-Markt. Falls GEO ausschließlich geografisch gemeint war, wird aus dem Prompt-Monitor ein Standort-Ranking — Aufwand ca. 1 Arbeitsschritt.

---

## 2. Gestaltungsthese

Zwei Anforderungen, die sich normalerweise widersprechen:

- **Apple-minimalistisch** — ruhige Flächen, präzise Typo-Hierarchie, keine Dekoration.
- **Geheimagent, aber seriös** — kein Matrix-Grün, kein Gamer-Neon.

Die Auflösung: **das Dossier**, nicht der Hacker-Terminal. Die Bildsprache kommt vom Lagebericht eines Nachrichtendienstes — Klassifizierungsleisten, Freigabestufe, Zeitstempel in Zulu-Zeit, Messing statt Neon, Mitternachtsblau statt Schwarz. Bond trägt Smoking, nicht Kapuzenpulli.

**Der ganze Mut steckt an einer Stelle:** im Zugangsbildschirm. Eine Iris-Blende, die sich beim Freischalten öffnet. Danach wird die Oberfläche still und arbeitet.

---

## 3. Farbpalette

### Variante A — `DOSSIER` (Standard, dunkel)
Mitternachtsblau mit Messing. Die Signatur der Marke.

| Token | Hex | Einsatz |
|---|---|---|
| `--ground` | `#0A1017` | Seitengrund, blaustichiges Fast-Schwarz |
| `--surface` | `#101A24` | Panels |
| `--line` | `#1E2B38` | Haarlinien, Panelrahmen |
| `--ink` | `#E8EEF4` | Primärtext |
| `--ink-2` | `#8A9DAF` | Sekundärtext, Achsen |
| `--accent` | `#D3A84C` | Messing — Marke, aktiver Zustand, Chart-Endpunkt |
| `--pos` | `#4FA88B` | positive Entwicklung (gedämpftes Petrolgrün) |
| `--neg` | `#C2534A` | negative Entwicklung (Oxidrot) |

### Variante B — `CUPERTINO` (hell, Apple)
Kühles Weiß, Frostglas, dieselbe Messing-Marke in dunklerer Sättigung.

| Token | Hex |
|---|---|
| `--ground` | `#F5F7F9` |
| `--surface` | `#FFFFFF` |
| `--line` | `#E1E7EC` |
| `--ink` | `#0B1219` |
| `--ink-2` | `#657686` |
| `--accent` | `#8A6714` |
| `--pos` / `--neg` | `#2E7D63` / `#B23A31` |

### Variante C — `GUNMETAL` (dunkel, monochrom)
Neutraler Waffenstahl, Radius 0, dichter gesetzt, Titel in Monospace. Instrumententafel statt Dokument.

| Token | Hex |
|---|---|
| `--ground` | `#0D0F10` |
| `--surface` | `#15181A` |
| `--line` | `#282D30` |
| `--ink` | `#EDEFF0` |
| `--ink-2` | `#8B9296` |
| `--accent` | `#DDE2E5` (das Licht selbst ist der Akzent) |
| `--pos` / `--neg` | `#7FA98C` / `#B4564B` |

### Variante D — `VELLUM` (hell, freigegebenes Dokument)
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

**Semantik ist vom Akzent getrennt.** Grün/Rot bedeuten immer nur Entwicklungsrichtung, nie Marke. Kein Wert wird ausschließlich über Farbe kodiert — jede Kennzahl trägt zusätzlich Vorzeichen und Pfeil.

---

## 4. Typografie

Drei Rollen, alle systemseitig verfügbar — bewusst **keine** Webfont-URL, weil die Artifact-Sandbox externe Schriftserver blockiert und ein stiller Fallback schlimmer aussieht als eine geplante Systemschrift.

| Rolle | Stack | Einsatz |
|---|---|---|
| **Display** | `Optima → Avenir Next → system-ui` | Wortmarke, Panel-Titel, KPI-Zahlen |
| **UI / Fließtext** | `-apple-system → SF Pro Text → Helvetica Neue` | Tabellen, Beschreibungen, Buttons |
| **Utility** | `SF Mono → Menlo → monospace` | Klassifizierungscodes, Zeitstempel, Achsen, Positionen |

Optima ist gemeißelt und wird auf Gedenktafeln und Urkunden verwendet — offiziell, ohne steif zu sein. Genau der Ton, den ein Lagebericht braucht. In `GUNMETAL` übernimmt die Monospace die Display-Rolle.

**Skala** (1.25 Major Third): 11 · 12 · 13 · 15 · 19 · 24 · 34 px
**Regeln:** Versal-Labels mit `0.14em` Laufweite · alle Zahlenspalten `tabular-nums` · Überschriften `text-wrap: balance`

---

## 5. Layout

Ein Raster, vier Varianten — die Varianten tauschen ausschließlich Tokens (Farbe, Radius, Schrift, Körnung), nie die Struktur. Deshalb bleibt jede Variante wartbar.

```
┌──────────────────────────────────────────────────────────────┐
│ VERTRAULICH · FREIGABESTUFE 2 · 2026-08-10 07:41Z    [Design▾]│  Klassifizierungsleiste
├──────────────────────────────────────────────────────────────┤
│ ROCFORTIS SIGNAL          Zeitraum: 12 Monate ▾    [Abmelden] │  Kopf
├──────────────────────────────────────────────────────────────┤
│ ┌──────┐┌──────┐┌──────┐ ┌──────┐┌──────┐┌──────┐            │
│ │ SEO  ││ SEO  ││ SEO  │ │ GEO  ││ GEO  ││ GEO  │            │  6 KPI-Kacheln
│ └──────┘└──────┘└──────┘ └──────┘└──────┘└──────┘            │  links SEO, rechts GEO
├───────────────────────────────────┬──────────────────────────┤
│ Sichtbarkeit über Zeit            │ KI-Engines               │
│ (zwei Reihen: SEO-Index / GEO-%)  │ (Zitationsanteil je       │
│                                   │  Engine, Balken + Δ)     │
├───────────────────────────────────┼──────────────────────────┤
│ Keyword-Lage (Tabelle)            │ Märkte & Regionen        │
├───────────────────────────────────┴──────────────────────────┤
│ PROMPT-MONITOR — überwachte KI-Anfragen, Zitat ja/nein        │  Signatur-Modul
├──────────────────────────────────────────────────────────────┤
│ Technische Basis: LCP · INP · CLS · Index · Crawl-Fehler      │
└──────────────────────────────────────────────────────────────┘
```

**Links SEO, rechts GEO** — die Trennung ist über die gesamte Seite konstant, damit der Blick sie nach dem ersten Scan nicht mehr suchen muss.

**Breakpoints:** 375 · 768 · 1024 · 1440 px. Tabellen scrollen in eigenem Container, der Seitenkörper nie horizontal.

---

## 6. Signatur-Elemente

1. **Die Iris.** Der Zugangsbildschirm öffnet sich beim Freischalten wie eine Blende. Eine einzige inszenierte Bewegung, danach Ruhe. Bei `prefers-reduced-motion` blendet sie ohne Rotation über.
2. **Der Prompt-Monitor.** Das Modul, das es auf keinem SEO-Dashboard gibt: die konkret überwachten KI-Anfragen, ob RocFortis zitiert wurde — und welcher Mitbewerber stattdessen. Das ist der eigentliche GEO-Wert und passt inhaltlich exakt zum Überwachungs-Motiv.
3. **Die Klassifizierungsleiste.** Freigabestufe und laufender Zulu-Zeitstempel. Trägt echte Information (Sitzungskontext), ist keine Dekoration.

---

## 7. Zugang

- **Benutzer:** `rocfortis`
- **Passwort:** wird separat übergeben — steht bewusst **nicht** in diesem Repository (siehe `ZUGANG.txt`, lokal und nicht versioniert).
- Der Nutzer wird einmalig angelegt. **Keine Selbstverwaltung, keine Passwortänderung, keine Registrierung** — es gibt bewusst keine entsprechende Oberfläche.
- Sitzung hält über `sessionStorage`; Schließen des Tabs meldet ab.
- Fünf Fehlversuche sperren die Eingabe für 60 Sekunden.
- Hinterlegt ist ein **SHA-256-Hash** (`c5a04f…654f`) über `benutzer:passwort:salt`, kein Klartext.

### Sicherheitseinstufung — bitte lesen

Das ist eine **clientseitige Zugangssperre**. Sie hält Gelegenheitszugriffe ab, ist aber keine echte Zugriffskontrolle: Wer die Seitenquelle öffnet, sieht den Hash und die Daten. Für die aktuelle Nutzung (Demodaten, interne Ansicht) ist das angemessen.

Solange die Seite über GitHub Pages aus einem **öffentlichen** Repository ausgeliefert wird, gilt zusätzlich: Die Seite ist für jeden erreichbar, der die URL kennt, und der Hash lässt sich offline auf das Passwort hin durchprobieren. Das Passwort ist damit eine Höflichkeitsbarriere, kein Schutz. Deshalb enthält die Seite ausschließlich Demodaten.

Sobald echte Kundenzahlen darin stehen, braucht es serverseitige Authentifizierung — konkret:

1. Statisches Hosting hinter Basic Auth oder Cloudflare Access, **oder**
2. Auslieferung über einen kleinen Server mit Session-Cookie und Passwort-Hash in der Datenbank (Argon2id), Daten erst nach erfolgreichem Login per API.

Ich setze das um, sobald das gewünscht ist.

---

## 8. Daten

Alle Zahlen sind **Demodaten** und im Dashboard als solche markiert (Chip `DEMODATEN` in der Kopfzeile). Sie liegen gesammelt in einem einzigen Objekt am Anfang des `<script>`-Blocks:

```js
const DATA = {
  kpis:     [...],   // 6 Kennzahlen-Kacheln
  timeline: {...},   // 12 Monate SEO-Index + GEO-Präsenz
  engines:  [...],   // Zitationsanteil je KI-Engine
  keywords: [...],   // Keyword-Tabelle
  regions:  [...],   // Märkte & Regionen
  prompts:  [...],   // Prompt-Monitor
  vitals:   [...]    // technische Basis
};
```

Zum Befüllen mit echten Zahlen wird nur dieses Objekt ersetzt — Layout, Charts und Tabellen leiten sich vollständig daraus ab.

**Quellen, die dafür angebunden werden sollten:** Google Search Console (SEO), Ahrefs oder Sistrix (Sichtbarkeitsindex), GA4 (Sitzungen), sowie ein GEO-Monitoring für den Prompt-Monitor (Peec AI, Otterly oder eigenes Prompt-Sampling gegen die Engine-APIs).

---

## 9. Qualitätsanforderungen

- [x] Kontrast ≥ 4.5:1 für Fließtext in allen vier Varianten
- [x] Tastaturbedienbar, Fokus überall sichtbar
- [x] `prefers-reduced-motion` respektiert
- [x] Keine Emoji als Icons — Inline-SVG
- [x] Übergänge 150–300 ms
- [x] Responsiv ab 375 px, kein horizontales Scrollen des Seitenkörpers
- [x] Läuft ohne Netzwerkzugriff (keine CDN-Abhängigkeit)

---

## 10. Offene Punkte

| # | Punkt | Entscheidung durch |
|---|---|---|
| 1 | GEO = Generative *oder* geografisch? Aktuell beides, Schwerpunkt generativ. | RocFortis |
| 2 | Branche der Demodaten ist als Sicherheits-/Infrastrukturdienstleistung angenommen — echte Keywords ersetzen. | RocFortis |
| 3 | Echte Datenanbindung (Search Console / GA4 / GEO-Monitoring) | nach Freigabe |
| 4 | Serverseitige Authentifizierung vor Einsatz mit echten Zahlen | vor Produktivbetrieb |
| 5 | Eigene Domain statt Artifact-URL | RocFortis |
