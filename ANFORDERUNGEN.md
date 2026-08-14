# Was wir von RocFortis brauchen

**Stand:** 14. August 2026
**Zweck:** Zugänge und Angaben, die für die SEO- und GEO-Optimierung von rocfortis.com nötig sind

Die Liste ist nach Dringlichkeit sortiert. Block 1 blockiert die Arbeit, ohne Block 2
bleiben Kennzahlen im Dashboard leer, Block 3 betrifft Inhalte.

---

## Block 1: Zugänge, ohne die nichts umgesetzt werden kann

### 1.1 WordPress-Administrator

Ein Benutzerkonto mit Administratorrechten auf rocfortis.com. Alternativ ein
Redakteurskonto plus getrennter Zugriff auf Theme und Plugins.

Gebraucht für: hreflang-Verweise, H1-Überschriften auf den Leistungsseiten,
Seitentitel, Meta-Beschreibungen, Alt-Texte, Yoast-Einstellungen.

### 1.2 Dateizugriff auf den Webserver

FTP, SFTP oder Zugang zum Hosting-Panel (Plesk, cPanel oder vergleichbar).

Gebraucht für: llms.txt im Wurzelverzeichnis ablegen, Caching einrichten,
CSS und JavaScript zusammenfassen.

### 1.3 Name des Hosting-Anbieters und des Tarifs

Die Serverantwort liegt bei 1,6 Sekunden, das ist etwa doppelt so lang wie der
Richtwert. Ob das am Tarif, am fehlenden Caching oder am Page-Builder liegt,
lässt sich nur mit dieser Angabe klären.

### 1.4 Übersetzungs-Setup

Wie wird die englische Fassung gepflegt? Über WPML, Polylang, eine
Mehrsprachigkeits-Funktion des Themes oder als eigenständige Seiten von Hand?

Davon hängt ab, ob die hreflang-Verweise mit einer Plugin-Einstellung erledigt
sind oder als Zuordnungstabelle im Theme hinterlegt werden müssen. Zeitunterschied:
ein halber gegenüber einem ganzen Arbeitstag.

---

## Block 2: Datenzugänge für das Dashboard

Ohne diese Zugänge bleiben mehrere Kennzahlen im Dashboard mit „k. A." markiert.
Alle drei werden lesend eingerichtet, es sind keine Schreibrechte nötig.

### 2.1 Google Search Console

Zugriff als „Nutzer mit vollständigen Rechten" oder „eingeschränkter Nutzer".

Liefert: Klicks, Impressionen, tatsächliche Suchbegriffe mit Position,
Indexierungsstatus je Seite, Core Web Vitals aus echten Nutzersitzungen
(LCP, INP, CLS), Crawling-Fehler.

Falls die Property noch nicht existiert, richten wir sie ein. Dafür genügt der
Dateizugriff aus Punkt 1.2.

### 2.2 Google Analytics 4

Leseberechtigung auf die Property.

Liefert: Besucherzahlen, Herkunftsländer und Regionen, Verweildauer,
Absprungrate, welche Seiten Anfragen auslösen.

Ohne GA4 zeigt das Panel „Märkte und Regionen" nur die Sprachabdeckung der
Website, nicht die tatsächliche Besucherverteilung.

### 2.3 Optional: Sistrix, Ahrefs oder Semrush

Falls RocFortis bereits ein solches Werkzeug im Einsatz hat, brauchen wir einen
Zugang oder einen Export. Liefert Suchvolumen, Sichtbarkeitsindex und das
Backlink-Profil. Ohne dieses Werkzeug bleiben die Spalten Volumen und
Veränderung in der Keyword-Tabelle leer.

Wenn kein Werkzeug vorhanden ist: Für die laufende Betreuung genügt Sistrix
Smart, das kostet etwa 25 Euro im Monat.

---

## Block 3: Inhaltliche Angaben

Diese Angaben stehen derzeit nirgends maschinenlesbar auf der Website. Sie fehlen
im Organization-Schema, weshalb KI-Systeme „RocFortis Group" nicht als Unternehmen
erkennen, sondern nur als Zeichenkette.

### 3.1 Firmendaten für das Organization-Schema

- Vollständiger Firmenwortlaut laut Firmenbuch
- Firmenbuchnummer und zuständiges Gericht
- Vollständige Anschrift des Firmensitzes in Wien
- Gründungsjahr
- Telefonnummer und E-Mail-Adresse für Anfragen
- Mitarbeiterzahl, falls sie genannt werden darf
- Firmenlogo als PNG oder SVG, mindestens 512 mal 512 Pixel, auf transparentem
  Grund. Das Logo-Feld im Schema ist derzeit leer.

### 3.2 Profile für die Verknüpfung der Marke

Vollständige Adressen aller offiziellen Profile:

- LinkedIn (Unternehmensseite)
- X, Instagram, YouTube, falls vorhanden
- Wikidata- oder Wikipedia-Eintrag, falls vorhanden
- Profile bei Branchenverzeichnissen und Kammern

Diese Verweise verankern die Marke als Entität. Sie sind der wirksamste einzelne
Hebel für die Auffindbarkeit in KI-Antworten.

### 3.3 Standorte

Für Berlin, Istanbul und London: Handelt es sich um eigene Niederlassungen mit
Anschrift, um Partnerbüros oder um reine Einsatzgebiete? Nur echte
Niederlassungen bekommen eigene Standortseiten und Schema-Einträge.

Auffällig: Istanbul ist Standort, aber es gibt keine türkische Sprachfassung.
Ist der türkische Markt ein Ziel oder dient das Büro der Region?

### 3.4 Freigaben für die drei neuen Leistungsseiten

Der Sichtbarkeitstest zeigt: Bei Suchanfragen mit Kaufabsicht erscheint RocFortis
nicht. Für die drei wichtigsten Lücken brauchen wir je eine Leistungsseite:

1. Dual-Use-Beratung und Exportgenehmigungen
2. UAV-gestützte Aufklärung und Überwachung
3. Schutz vor Industrie- und Wirtschaftsspionage

Dafür wird gebraucht:

- Welche Leistung wird konkret erbracht, in welchem Umfang?
- Für welche Auftraggeber, mit welchem typischen Ablauf?
- Was darf öffentlich stehen und was nicht? Bei Verteidigungsthemen ist das die
  entscheidende Frage.
- Referenzen oder anonymisierte Fallbeispiele, falls freigegeben
- Ansprechpartner für Rückfragen zum Fachinhalt

### 3.5 Redaktionelle Zuständigkeit

Die letzte Änderung an der Website datiert vom April 2026, das sind vier Monate
Stillstand. Perplexity und andere KI-Systeme gewichten Aktualität stark.

Wer schreibt künftig Fachbeiträge, und in welchem Rhythmus? Ein Beitrag pro Monat
genügt, aber er sollte verlässlich kommen.

---

## Block 4: Entscheidungen

### 4.1 Dürfen Alt-Texte automatisch vorgeschlagen werden?

457 von 476 Bildern haben keinen Alt-Text. Wir können Vorschläge erzeugen und zur
Durchsicht vorlegen, oder RocFortis schreibt sie selbst. Ersteres ist deutlich
schneller, braucht aber eine Freigaberunde.

### 4.2 Wer setzt um?

Drei Möglichkeiten: Wir setzen alles um, RocFortis setzt nach unserer Anleitung
um, oder wir teilen auf (Technik bei uns, Inhalte bei RocFortis).

### 4.3 Umgang mit dem Dashboard

Soll das Lagebild bei RocFortis liegen und regelmäßig aktualisiert werden? Dann
brauchen wir eine Entscheidung über Hosting und Zugangsschutz. Die derzeitige
Passwortabfrage ist eine Sperre für Gelegenheitszugriffe, keine echte
Zugriffskontrolle.

---

## Kurzfassung für die erste Rückmeldung

Wenn RocFortis nur drei Dinge liefern kann, dann diese:

1. WordPress-Administratorzugang
2. Lesezugriff auf Google Search Console
3. Firmendaten und Profiladressen aus den Punkten 3.1 und 3.2

Damit sind die drei kritischen Befunde behebbar und das Dashboard füllt sich mit
echten Suchdaten.
