# SEO- und GEO-Audit rocfortis.com

**Erhebung:** 12. August 2026
**Umfang:** Vollcrawl aller 98 Sitemap-URLs, Auswertung der ausgelieferten HTML-Dokumente, Browser-Messung der Ladezeiten, sechs echte Suchabfragen
**Ergebnis:** SEO 54/100 · GEO 55/100 (Note C)

---

## Kurzfassung

Die technische Grundlage ist solider als bei den meisten Websites dieser Größe: 98 von 98 Seiten antworten mit Status 200, jede hat einen selbstreferenzierenden Canonical, keine trägt versehentlich ein `noindex`, die interne Verlinkung ist dicht (Median 84 Links pro Seite), und die Inhalte sind ungewöhnlich tief: Median 909 Wörter, keine einzige dünne Seite. Yoast liefert auf jeder Seite ein Grundgerüst an strukturierten Daten.

Was die Bewertung drückt, sind wenige, klar benennbare Lücken. Drei davon wiegen schwer, und alle drei sind reparierbar, ohne die Website umzubauen:

1. **Die Website ist zweisprachig, sagt es Google aber nicht.** Auf keiner der 98 Seiten steht ein `hreflang`-Verweis. Die deutsche und die englische Fassung derselben Seite konkurrieren dadurch gegeneinander.
2. **Die fünf Leistungsseiten haben keine H1.** SEA, AIR, LAND, SUPPLY und INTEL, also die Seiten mit je rund 900 Wörtern, auf denen das Geschäft erklärt wird, benennen ihr Hauptthema in keiner Überschrift erster Ordnung.
3. **457 von 476 Bildern haben keinen Alt-Text.** 96 Prozent. Für Suchmaschinen und für KI-Systeme sind diese Bilder Leerstellen.

Der Sichtbarkeitstest zeigt das Muster dahinter: RocFortis wird gefunden, wenn jemand die Marke oder ein Fachthema sucht, zu dem ein eigener Artikel existiert. Bei generischen Anbieteranfragen, also genau dort, wo Kaufabsicht steckt, erscheinen andere.

---

## 1. Was gut funktioniert

| Befund | Wert |
|---|---|
| Erreichbarkeit | 98 von 98 Seiten Status 200, keine Weiterleitungsketten, kein 404 |
| Canonical | 98 von 98 selbstreferenzierend |
| Indexierbarkeit | keine Seite trägt `noindex` |
| Inhaltstiefe | Median 909 Wörter, Mittel 1.161, keine Seite unter 300 Wörtern |
| Interne Verlinkung | Median 84 interne Links pro Seite, keine verwaisten Seiten |
| Sitemap | vier saubere Teilsitemaps mit Änderungsdatum, korrekt in robots.txt verwiesen |
| KI-Crawler | GPTBot, ClaudeBot, PerplexityBot und alle anderen sind zugelassen |
| Strukturierte Daten | Organization, WebSite, BreadcrumbList auf allen Seiten; Article auf 56 |

Der letzte Punkt verdient Betonung: Viele Unternehmen sperren KI-Crawler versehentlich aus und wundern sich dann über fehlende Sichtbarkeit. Hier ist der Zugang offen, die Grundlage stimmt also.

---

## 2. Kritische Befunde

### 2.1 hreflang fehlt auf allen 98 Seiten

**Gemessen:** 0 von 98 Seiten enthalten ein `hreflang`-Element. Die Sprachkennzeichnung im `<html>`-Tag ist zwar korrekt gesetzt (51× `de-DE`, 47× `en-US`), aber die Seiten verweisen nicht aufeinander.

**Warum das zählt:** Google erfährt nirgends, dass `/capability/sea-maritime-sicherheit…` und `/en/capability/sea-maritime-safety…` dieselbe Seite in zwei Sprachen sind. Beide werden als eigenständige Dokumente behandelt und konkurrieren um dieselbe Position. Zusätzlich kann Google einem englischsprachigen Suchenden die deutsche Fassung ausliefern.

**Behebung:** In jede Seite drei Verweise aufnehmen: auf sich selbst, auf die Schwestersprache und einen `x-default`:

```html
<link rel="alternate" hreflang="de" href="https://rocfortis.com/capability/sea-maritime-sicherheit-schutz-kritischer-seeinfrastruktur/">
<link rel="alternate" hreflang="en" href="https://rocfortis.com/en/capability/sea-maritime-safety-protection-of-critical-maritime-infrastructure/">
<link rel="alternate" hreflang="x-default" href="https://rocfortis.com/">
```

Bei WordPress übernimmt das ein Übersetzungs-Plugin (WPML, Polylang) automatisch, sobald die Sprachpaare verknüpft sind. Falls die englische Fassung ohne solches Plugin gepflegt wird, lassen sich die Verweise über `wp_head` aus einer Zuordnungstabelle ausgeben.

**Aufwand:** halber Tag, wenn die Paare bereits verknüpft sind. Sonst ein Tag.

---

### 2.2 Keine H1 auf den Leistungsseiten

**Gemessen:** 16 Seiten ohne H1, darunter alle zehn Capability-Seiten (fünf deutsch, fünf englisch):

| Seite | Wörter | H1 |
|---|---|---|
| SEA: Maritime Sicherheit | 902 | fehlt |
| AIR: Aufklärung, Überwachung | 906 | fehlt |
| LAND: Grenzschutz, Robotik | 913 | fehlt |
| SUPPLY: Projektentwicklung | 916 | fehlt |
| INTEL: Aufklärung, Analyse | 883 | fehlt |

Diese Seiten sind inhaltlich stark, rund 900 Wörter zu einem klar abgegrenzten Thema. Sie sagen nur nicht in der wichtigsten Überschrift, worum es geht.

**Warum das zählt:** Die H1 ist für Suchmaschinen und KI-Systeme das stärkste Signal, worum eine Seite geht. Fehlt sie, muss die Maschine das Thema aus dem Fließtext erraten. Bei Seiten, die das Kerngeschäft erklären, ist das eine vermeidbare Schwäche.

**Behebung:** Je Seite eine H1 mit dem Kernbegriff. Vorschläge:

| Seite | H1 |
|---|---|
| SEA | Maritime Sicherheit und Schutz kritischer Seeinfrastruktur |
| AIR | Luftgestützte Aufklärung und Überwachung |
| LAND | Grenzschutz, Robotik und urbane Überwachung |
| SUPPLY | Verteidigungstechnologie und Systemvertrieb |
| INTEL | Aufklärung, Analyse und Intervention |

Wahrscheinlich ist die Überschrift im Template als `<div>` oder `<h2>` ausgezeichnet. Dann genügt eine Änderung im Capability-Template statt fünf Einzelbearbeitungen.

**Aufwand:** zwei Stunden.

---

### 2.3 457 von 476 Bildern ohne Alt-Text

**Gemessen:** 96 Prozent aller Bilder haben kein `alt`-Attribut oder ein leeres. Die schwersten Fälle:

| Seite | Bilder ohne Alt |
|---|---|
| /offerings/ und /en/offerings/ | je 35 von 35 |
| /news/ und /en/news/ | 10 bzw. 11 von 12 |
| Fachartikel | typisch 6 von 6 |

**Warum das zählt:** Drei Gründe, in dieser Reihenfolge. Erstens Barrierefreiheit: Screenreader-Nutzer erfahren nicht, was abgebildet ist, und die Website eines Unternehmens, das mit Behörden arbeitet, sollte hier sauber sein. Zweitens: KI-Systeme lesen keine Bilder, sie lesen Alt-Texte. Drittens Bildersuche.

**Behebung:** Die 35 Bilder auf der Offerings-Seite sind vermutlich Branchen-Symbole und schnell beschrieben. Für den Bestand empfiehlt sich ein Durchgang in der Mediathek, sortiert nach Verwendungshäufigkeit. Die 50 meistgenutzten Bilder decken erfahrungsgemäß den Großteil ab.

Alt-Texte beschreiben, was zu sehen ist, nicht was das Bild bewirken soll: „Kontrollraum mit sechs Monitoren und zwei Operatoren" statt „Sicherheit Überwachung Wien".

**Aufwand:** ein bis zwei Tage für den Bestand, danach Teil der Redaktionsroutine.

---

## 3. Hohe Priorität

### 3.1 Logo-Feld im Organization-Schema ist leer

**Gemessen:** Das JSON-LD auf jeder Seite enthält:

```json
"logo": { "@type": "ImageObject", "url": "", "contentUrl": "", "caption": "RocFortis Group" }
```

Beide URL-Felder sind leer. Zusätzlich fehlen im Organization-Objekt: `sameAs`, `description`, `address`, `contactPoint`, `foundingDate`, `legalName`.

**Warum das zählt:** `sameAs` ist der Verweis, mit dem eine Marke als Entität verankert wird, also die Verknüpfung zu LinkedIn, Wikidata oder Handelsregister. Ohne diese Verweise ist „RocFortis Group" für ein KI-System eine Zeichenkette, kein Unternehmen. Das erklärt einen erheblichen Teil des GEO-Rückstands.

**Behebung:** In Yoast unter *SEO → Darstellung in der Suche → Allgemein* das Logo hinterlegen und die Social-Profile eintragen. Vollständiges Zielbild:

```json
{
  "@type": "Organization",
  "name": "RocFortis Group",
  "legalName": "RocFortis Group",
  "url": "https://rocfortis.com/",
  "logo": { "@type": "ImageObject", "url": "https://rocfortis.com/pfad/logo.png",
            "width": 512, "height": 512 },
  "description": "Strategische Beratung für Sicherheit, Risikomanagement und Krisenreaktion",
  "foundingDate": "JJJJ",
  "address": { "@type": "PostalAddress", "addressLocality": "Wien",
               "addressCountry": "AT", "streetAddress": "…", "postalCode": "…" },
  "contactPoint": { "@type": "ContactPoint", "contactType": "Vertrieb",
                    "email": "…", "telephone": "…", "availableLanguage": ["de","en"] },
  "sameAs": [
    "https://www.linkedin.com/company/…",
    "https://www.wikidata.org/wiki/…"
  ]
}
```

**Aufwand:** zwei Stunden, größtenteils in der Yoast-Oberfläche.

---

### 3.2 81 von 98 Titeln sind zu lang

**Gemessen:** 82 Prozent der Titel überschreiten 60 Zeichen; der längste hat 124. Median 70. Außerdem drei doppelte Titel: *Offerings*, *RocUnits* und *Privacy Policy* jeweils zweimal, weil die deutsche und die englische Fassung denselben Titel tragen.

**Warum das zählt:** Google schneidet nach etwa 60 Zeichen ab. Bei 124 Zeichen ist die Hälfte unsichtbar, und häufig verschwindet gerade der Teil, der den Klick auslösen würde.

**Beispiel:**

> Ist: `Die nächste Sicherheitsrevolution: Wie sich Sicherheitssysteme in den nächsten 10 Jahren entwickeln werden - RocFortis Group` (124)
> Besser: `Sicherheitssysteme 2035: Was sich ändert | RocFortis` (52)

**Behebung:** Priorisiert vorgehen, zuerst die zehn Capability- und die 32 Branchenseiten, danach die Fachartikel. Die drei Titeldubletten sofort auflösen, indem die englischen Fassungen einen eigenen Titel bekommen.

**Aufwand:** ein Tag für die wichtigsten 40 Seiten.

---

### 3.3 Serverantwort 1,6 Sekunden, CSS 1 Megabyte

**Gemessen (Browser, Startseite):**

| Messwert | Wert | Richtwert |
|---|---|---|
| Serverantwort (TTFB) | 1.642 ms | unter 800 ms |
| Seite vollständig geladen | 4.086 ms | unter 2.500 ms |
| CSS | 1.077 KB über 4 Dateien | unter 150 KB |
| JavaScript | 166 KB über 24 Dateien | Dateizahl reduzieren |
| Ressourcen gesamt | 61 | |

Im Crawl über alle 98 Seiten: Median 1.972 ms, Maximum 4.532 ms. 44 Seiten brauchen über zwei Sekunden.

**Warum das zählt:** Ein Megabyte CSS ist außergewöhnlich viel, üblich sind 50 bis 150 KB. Der Wert deutet auf einen Page-Builder hin, der die Stile aller Module ausliefert, auch die ungenutzten. Die 1,6 Sekunden Serverantwort entstehen vor dem ersten Byte, sind also unabhängig davon, wie schnell der Besucher angebunden ist.

**Behebung, nach Wirkung geordnet:**

1. **Serverseitiges Caching** (WP Rocket, LiteSpeed Cache oder Cloudflare APO). Bringt die Serverantwort typischerweise unter 300 ms. Größter Hebel, geringster Aufwand.
2. **Ungenutztes CSS entfernen.** Die meisten Caching-Plugins können das automatisch je Seitentyp.
3. **JavaScript-Dateien zusammenfassen**, 24 Einzeldateien sind zu viele.
4. **Bilder auf WebP umstellen** und `loading="lazy"` setzen.

**Aufwand:** Punkt 1 an einem halben Tag; Punkte 2 bis 4 ein bis zwei Tage mit Testdurchläufen.

---

## 4. Mittlere Priorität

### 4.1 Zehn Seiten ohne Meta-Beschreibung

Betroffen sind überwiegend Fachartikel, unter anderem:

- `/dual-use-technologien-wo-liegen-die-chancen-und-risiken-fuer-sicherheit-wirtschaft/`
- `/groenland-im-fokus-trump-arktis-strategie-und-die-neue-nato-frontlinie/`
- `/maschinen-identitaeten-ki-agenten-die-unsichtbare-risikoflaeche-2025/`
- `/industriespionage-4-0-wie-sich-unternehmen-gegen-digitale-angriffe-schuetzen-koennen/`
- dieselben Artikel in der englischen Fassung

Fehlt die Beschreibung, setzt Google einen beliebigen Textausschnitt ein. 38 der vorhandenen Beschreibungen sind zudem länger als 160 Zeichen und werden gekürzt; die längste hat 431.

### 4.2 Kein llms.txt

`https://rocfortis.com/llms.txt` liefert 404. Die Datei ist eine schlichte Textdatei im Wurzelverzeichnis, die KI-Systemen erklärt, was das Unternehmen macht und welche Seiten die wichtigsten sind. Sie ist noch kein verbindlicher Standard, aber billig anzulegen und wird zunehmend ausgewertet. Ein Entwurf liegt als [llms.txt](llms.txt) bei; er muss nur um Kontaktdaten und Gründungsjahr ergänzt und hochgeladen werden.

### 4.3 Kein FAQ- oder Service-Schema

Die Website nutzt ausschließlich das Yoast-Grundgerüst. Für ein Beratungsunternehmen fehlen zwei Auszeichnungen:

- **Service** auf den fünf Capability-Seiten. Macht maschinell lesbar, welche Leistung mit welchem Einsatzgebiet angeboten wird.
- **FAQPage** dort, wo Fragen beantwortet werden. Das ist der mit Abstand direkteste Weg in KI-Antworten, weil Frage-Antwort-Paare genau das Format sind, das diese Systeme zitieren.

---

## 5. Sichtbarkeitstest

Sechs Suchanfragen, am 12. August 2026 tatsächlich abgesetzt. „Gefunden" bedeutet: rocfortis.com steht in den Ergebnissen.

| Anfrage | Art | Ergebnis | Platz | Stattdessen |
|---|---|---|---|---|
| RocFortis Group Sicherheit Verteidigung Österreich | Marke | gefunden | 1 | keiner |
| OSINT Frühwarnsystem geopolitische Risiken | Fachthema | gefunden | 1 | keiner |
| Maritime Sicherheit kritische Unterwasserinfrastruktur | Fachthema | gefunden | 7 | keiner |
| Dual-Use Ausfuhrgenehmigung Beratung | Kaufabsicht | nicht gefunden | k. A. | Rödl & Partner, WINHELLER |
| Drohnen UAV Aufklärung KI Österreich | Kaufabsicht | nicht gefunden | k. A. | ProSafe, PSM Austria |
| Industriespionage Schutz Beratung Risikoanalyse | Kaufabsicht | nicht gefunden | k. A. | SIUS Consulting, WDS |

**Das Muster:** Drei von drei Treffern bei Marken- und Fachthemenanfragen, null von drei bei Anfragen mit Kaufabsicht. Die Fachartikel funktionieren, sie ranken für ihr Thema. Was fehlt, sind Seiten, die eine Leistung als Angebot beschreiben statt als Fachthema.

Bemerkenswert ist der Fall Dual-Use: RocFortis hat einen ausführlichen Artikel zum Thema, wird aber bei der Anbietersuche nicht gefunden, und zwar gegen Kanzleien, die eine Leistungsseite dazu haben. Der Inhalt ist da, nur im falschen Format.

**Einschränkung:** Dies sind Websuchergebnisse, nicht direkt Antworten von ChatGPT oder Perplexity. Da diese Systeme auf Websuche aufsetzen, ist es ein belastbarer Näherungswert. Für echte Zitationsmessung braucht es ein GEO-Monitoring.

---

## 6. Maßnahmenplan

### Woche 1: Fundament

| Maßnahme | Aufwand | Wirkung |
|---|---|---|
| hreflang auf allen Seiten | 0,5 bis 1 Tag | beendet die Sprachkonkurrenz |
| H1 auf den zehn Capability-Seiten | 2 Std. | benennt das Kerngeschäft |
| Logo und `sameAs` im Organization-Schema | 2 Std. | verankert die Marke als Entität |
| Serverseitiges Caching aktivieren | 0,5 Tag | Antwortzeit unter 300 ms |
| llms.txt hochladen | 15 Min. | Einstiegskarte für KI-Systeme |

### Wochen 2 bis 3: Substanz

| Maßnahme | Aufwand |
|---|---|
| Titel der 40 wichtigsten Seiten kürzen, drei Dubletten auflösen | 1 Tag |
| Alt-Texte für den Bildbestand | 1 bis 2 Tage |
| Zehn fehlende Meta-Beschreibungen ergänzen | 2 Std. |
| Ungenutztes CSS entfernen, JavaScript bündeln | 1 bis 2 Tage |

### Monat 2: Sichtbarkeit dort, wo gekauft wird

Der eigentliche Hebel. Für die drei verlorenen Anfragen je eine Leistungsseite anlegen, nicht als Fachartikel, sondern als Angebot: Was wird geliefert, für wen, in welchem Rahmen, mit welchem nächsten Schritt.

1. Dual-Use-Beratung und Exportgenehmigungen
2. UAV-gestützte Aufklärung und Überwachung
3. Schutz vor Industriespionage und Wirtschaftsspionage

Jede mit `Service`-Schema und einem FAQ-Block aus echten Kundenfragen. Bestehende Fachartikel dorthin verlinken. Die Autorität ist vorhanden und wird derzeit nicht auf ein Angebot geleitet.

### Laufend

Zweite Erhebung nach vier Wochen. Dieser Audit ist der Nullpunkt; erst der zweite Durchlauf zeigt Bewegung. Dann bekommt das Dashboard auch seinen Zeitverlauf.

---

## 7. Was diese Erhebung nicht enthält

Ehrlichkeitshalber, damit die Zahlen richtig eingeordnet werden:

| Nicht erhoben | Weil | Nötig dafür |
|---|---|---|
| Besucherzahlen, Klicks, Impressionen | kein Zugang | Search Console, GA4 |
| Keyword-Positionen und Suchvolumen | kein Zugang | Search Console oder Sistrix/Ahrefs |
| LCP, INP, CLS aus echten Nutzersitzungen | nur Labormessung möglich | CrUX-Feldwerte über die Search Console |
| Zitationen in ChatGPT, Perplexity, Claude | keine Messinfrastruktur | GEO-Monitoring oder eigenes Prompt-Sampling |
| Backlink-Profil | kein Zugang | Ahrefs, Majestic oder Moz |
| Entwicklung über Zeit | erste Messung | zweite Erhebung |

Die Bewertungen 54/100 und 55/100 beruhen auf dem, was von außen messbar ist. Mit Search-Console-Zugang wird das Bild genauer, die drei kritischen Befunde ändern sich dadurch aber nicht.

---

## Methodik

- **Crawl:** alle 98 URLs aus `sitemap_index.xml` (post, page, capability, offering), robots.txt beachtet, vier gleichzeitige Verbindungen
- **Ausgewertet:** Statuscode, Titel, Meta-Beschreibung, Canonical, Robots-Anweisung, Sprache, hreflang, Überschriftenstruktur, Wortzahl, Bilder und Alt-Texte, JSON-LD, interne und externe Links, Antwortzeit, Dokumentgröße
- **Ladezeit:** Navigation-Timing- und Resource-Timing-API im Browser, Startseite ungecacht
- **Sichtbarkeit:** sechs Suchabfragen, Ergebnisseiten manuell auf rocfortis.com geprüft
- **Bewertung:** SEO nach sieben gewichteten Kategorien (Inhalt 23 %, Technik 22 %, On-Page 20 %, Schema 10 %, Ladezeit 10 %, KI-Auffindbarkeit 10 %, Bilder 5 %); GEO nach dem Drei-Schichten-Modell (Zitierfähigkeit 35 %, Marke 25 %, Technik 20 %, strukturierte Daten 20 %)
