# Absicherung vor dem Einsatz mit echten Zahlen

**Stand:** 15. August 2026
**Betrifft:** `index.html`, ausgeliefert über GitHub Pages

---

## Wo wir gerade stehen

Die Seite hat eine Passwortabfrage. Die läuft vollständig im Browser: Im
Quelltext steht ein SHA-256-Hash über `benutzer:passwort:salt`, und JavaScript
vergleicht die Eingabe damit.

Das hält Gelegenheitszugriffe ab. Zugriffskontrolle ist es nicht:

| Was jemand tun kann | Warum das geht |
|---|---|
| Den Quelltext öffnen und alle Daten lesen | Die Zahlen stehen im Objekt `DATA`, ausgeliefert wird die ganze Datei |
| Den Hash offline durchprobieren | SHA-256 ohne Schlüsselstreckung, eine gewöhnliche Grafikkarte schafft Milliarden Versuche pro Sekunde |
| Die Sperre im Browser umgehen | Die Prüfung findet im Browser statt, nicht auf dem Server |

Solange nur die Erhebung vom 12. August 2026 drinsteht, ist das vertretbar. Alle
Zahlen darin stammen aus öffentlich abrufbaren Quellen: der Website selbst und
Suchergebnissen. Was jemand erfährt, ist die Bewertung der Website.

**Sobald Zahlen aus der Search Console oder aus GA4 dazukommen, ändert sich
das.** Besucherzahlen, Klicks und Umsatzsignale sind Geschäftszahlen. Ab dann
reicht die aktuelle Lösung nicht mehr.

---

## Empfehlung: Cloudflare Access

Für eine Seite, die eine Handvoll Personen nutzt, ist das der beste Schnitt aus
Aufwand und Sicherheit. Die Prüfung passiert vor der Auslieferung, nicht im
Browser. Wer nicht angemeldet ist, bekommt die Datei nie zu sehen.

Der kostenlose Tarif deckt bis zu 50 Nutzer ab. Für diesen Fall genügt das.

### Was dafür nötig ist

1. Eine Domain, die bei Cloudflare liegt, etwa `signal.rocfortis.com`
2. Ein Cloudflare-Konto mit Zugriff auf diese Domain
3. Fünfzehn bis dreißig Minuten

### Schritte

1. **Domain zu Cloudflare bringen.** Nameserver beim Registrar auf Cloudflare
   umstellen. Falls `rocfortis.com` schon dort liegt, entfällt der Schritt.

2. **Seite hinter die Domain hängen.** Zwei Wege:
   - Cloudflare Pages, das Repository direkt verbinden. Empfehlenswert, weil
     GitHub Pages danach ganz entfallen kann.
   - Oder GitHub Pages behalten und `signal.rocfortis.com` als Custom Domain
     eintragen, mit CNAME auf die GitHub-Pages-Adresse.

3. **Zero Trust einrichten.** Im Cloudflare-Dashboard unter *Zero Trust →
   Access → Applications* eine Anwendung vom Typ *Self-hosted* anlegen:
   - Domain: `signal.rocfortis.com`
   - Session-Dauer: 24 Stunden ist ein guter Startwert

4. **Regel definieren.** Eine Policy vom Typ *Allow*, als Kriterium
   *Emails* mit den Adressen, die Zugriff bekommen sollen. Für den Eigentümer
   reicht eine einzige Adresse.

5. **Anmeldeweg wählen.** Unter *Settings → Authentication*:
   - **One-time PIN** braucht keinerlei Vorbereitung. Cloudflare schickt einen
     Code per E-Mail. Für einen Einzelnutzer völlig ausreichend.
   - **Microsoft Entra ID** oder **Google Workspace**, falls RocFortis so etwas
     ohnehin betreibt. Dann greifen die dortigen Regeln inklusive
     Zwei-Faktor-Authentifizierung.

6. **Passwortabfrage aus der Datei entfernen.** Zwei Sperren hintereinander
   nerven, und die schwächere suggeriert Sicherheit, die sie nicht liefert.
   Sobald Access steht, fliegt der Gate-Block raus. Sag Bescheid, dann mache
   ich das.

7. **Repository auf privat stellen.** Sonst liegt die Datei mitsamt Zahlen
   weiterhin öffentlich auf GitHub, egal was vor der Domain steht.

### Was das kostet

k. A. für Access selbst im kostenlosen Tarif. Die Domain kostet, was sie beim
Registrar kostet. Cloudflare Pages ist für dieses Datenvolumen ebenfalls
kostenlos.

---

## Alternative: eigener Server mit Sitzung

Sinnvoll, wenn die Daten später per Schnittstelle nachgeladen werden sollen,
statt fest in der Datei zu stehen.

| Baustein | Wahl |
|---|---|
| Passwort-Hash | Argon2id, nicht SHA-256 |
| Sitzung | Cookie mit `HttpOnly`, `Secure`, `SameSite=Strict` |
| Daten | erst nach erfolgreicher Anmeldung über eine API ausliefern, nie im HTML |
| Fehlversuche | serverseitig zählen und sperren, nicht im Browser |

Das ist die saubere Lösung, kostet aber Betrieb: ein Server, der läuft,
aktualisiert wird und überwacht werden muss. Für ein Dashboard, das eine Person
öffnet, steht das in keinem Verhältnis. Deshalb die Empfehlung oben.

---

## Was auf keinen Fall reicht

- **Die URL geheim halten.** Adressen tauchen in Verläufen, Lesezeichen und
  Weiterleitungs-Headern auf. Das ist kein Schutz.
- **Das Passwort im Quelltext verschleiern.** Egal wie, es wird ausgeliefert.
- **`robots.txt` oder `noindex`.** Das hält Suchmaschinen fern, keine Menschen.
  Beides ist in der Datei gesetzt, aber als Hygiene, nicht als Schutz.

---

## Reihenfolge

Wenn echte Zahlen dazukommen sollen, in dieser Folge:

1. Repository auf privat stellen, sofort, unabhängig vom Rest
2. Domain und Cloudflare Access einrichten
3. Passwortabfrage aus der Datei entfernen
4. Erst danach Search-Console- und GA4-Zahlen einbauen

Punkt 4 vor Punkt 1 bis 3 wäre der Fehler, den man später nicht mehr rückgängig
machen kann: Was einmal öffentlich stand, war öffentlich.
