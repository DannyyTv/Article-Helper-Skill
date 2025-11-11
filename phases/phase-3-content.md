# Phase 3: Content-Erstellung

## Zweck

Diese Phase erstellt den vollständigen Artikel-Content basierend auf Phase 2 Outline. Der Agent arbeitet **abschnittweise** (H2 für H2) zusammen mit dem User, um hochqualitativen, strukturierten Content zu generieren. Formatierung (Design, Abstände, HTML) erfolgt NICHT in Phase 3 - nur Content und logische Struktur (H2, H3, H4, Listen, Boxen-Konzepte).

**OUTPUT:** `/Articles/[keyword-slug]/content/content.md`

---

## Tools in Phase 3

**Die KI nutzt FOLGENDE Tools in dieser Phase:**

| Schritt | Tool | Funktion | Optional |
|---------|------|----------|----------|
| 1 | Read (lokal) | Phase 1 + Phase 2 Daten laden | Nein |
| 2 | WebFetch | Referenz-Artikel abrufen (URL) | Nein |
| 3 | Claude (intern) | Content-Outline vorbereiten | Nein |
| 4+ | Read/Write/Edit | `.md` Dateien verwalten | Nein |
| 5.5 | WebFetch | Quellen recherchieren (On-Demand) | Ja |

**Obligatorisch:** Lokale Read (Phase 1 + 2), lokale `.md` Verwaltung
**Optional:** WebFetch (Quellen-Recherche während Content-Erstellung in Schritt 5.5) Wenn Quellen recherchiert werden, dann müssen sie in Phase 2: `/Articles/[keyword-slug]/outline/outline.md` ergänzt werden.

---

## ⚡ WICHTIG: Was die KI konkret tun muss

**NICHT NUR:** Content schreiben und zeigen
**SONDERN:**:
1. Phase 1 + Phase 2 Daten lokal zu laden (Schritt 1)
2. Referenz-Artikel via WebFetch abrufen für Style-Guide (Schritt 2)
3. Kontext & Outline präsentieren (Schritt 3)
4. **ABSCHNITTWEISE** Content-Erstellung (NICHT alles auf einmal!)
5. **OPTIONAL: Pro H2 fragen ob Quellen recherchiert werden sollen** (Schritt 5.5)
6. Lokale `.md` Datei in `/Articles/[keyword-slug]/content/` verwenden
7. "Kurz zusammengefasst" Box am Schluss erstellen
8. Finalen kompletten Artikel lokal speichern

**Wann eine Phase 3 Session beendet wird:**
- Der komplette Artikel (Markdown) MUSS in `/Articles/[keyword-slug]/content/content.md` gespeichert sein
- User kann später Phase 4 (Validierung) starten
- Alles ist persistent, nichts ist verloren

---

## Workflow

### Schritt 1: Phase 1 + Phase 2 Daten laden

**Tool:** Lokale Read

**Die KI MUSS FOLGENDES TUN:**

1. Frage User nach `keyword-slug` (oder verwende aktive Session)
2. Lade beide Dateien lokal:
   - Lese `/Articles/[keyword-slug]/research/research.md`
   - Lese `/Articles/[keyword-slug]/outline/outline.md`

3. Parse die Daten:
   - Phase 1: Opportunities, Content Gaps, Key Insights
   - Phase 2: Komplettes Outline (alle H2 Titel + H3 Punkte)

---

### Schritt 2: Referenz-Artikel abrufen

**Tool:** Lokale `.md` Datei

**Die KI MUSS FOLGENDES TUN:**

1. Lese `ReferenceArticle.md` um die um Beispiel-Artikeln zu verstehen (Ton, Struktur, Content-Stil, Beispiele, etc.)
2. Lese `../content-design-guide.md` für H2-Layout, Info-Box-Variation, Links, Keywords, FAQ, Fazit

---

### Schritt 3: Kontext präsentieren

**Die KI MUSS dem User FOLGENDES ZEIGEN:**

```markdown
## 📋 Phase 3: Content-Erstellung

**Projekt:** [Titel aus Phase 1]
**Keyword:** [Keyword]

### Geplante Struktur (aus Phase 2 Outline):

**Einleitung** (100-150 Wörter)

**Hauptabschnitte:**
1. H2: [Titel]
   - H3: [Unterpunkt]
   - H3: [Unterpunkt]

2. H2: [Titel]
   - H3: [Unterpunkt]

... (alle H2s auflisten)

**Kurz zusammengefasst Box** (nach Einleitung, 3-4 Punkte)
**FAQ** (3-5 Fragen)
**Fazit**

---

### Top Opportunities aus Phase 1:
- Opportunity 1: [konkret]
- Opportunity 2: [konkret]
- Opportunity 3: [konkret]

---

### Schritt 4: Einleitung schreiben (ZUERST!)

**Die KI MUSS FOLGENDES TUN:**

1. Schreibe Einleitung (100-150 Wörter):
   - Conversational, Du-Form
   - Problem/Nutzen klar machen
   - Hook: "Du suchst nach..."
   - Maximal 3-4 Absätze

2. Zeige Entwurf:
```markdown
# [H1 Titel]

[Einleitung hier...]
```

3. Frage User:
```
Passt die Einleitung so? (OK / Feedback: [änderung])
```

4. User-Antwort:
   - "OK" → Weiter zu Schritt 5
   - "Feedback: ..." → Revisieren, Schritt 4 wiederholen

5. **Speichern in `.md`:**
   - Erstelle `/Articles/[keyword-slug]/content/content.md`
   - Inhalt: Einleitung + Outline der restlichen H2s (als Platzhalter)

```markdown
# [H1 Titel]

[Einleitung komplett]

---

## [H2 1 Titel]
(wird noch geschrieben)

## [H2 2 Titel]
(wird noch geschrieben)

...
```

---

### Schritt 5: H2 Abschnitte schreiben (ITERATIV, EINZELN)

**Die KI MUSS FOLGENDES TUN:**

1. Frage User für jeden H2:
```
Sollen wir jetzt H2 '[Titel]' schreiben?
(basierend auf Phase 2 Outline: [H3 Punkte auflisten])
```

2. User genehmigt oder überspringt

3. **SCHREIBE DEN H2:**
   - Basierend auf Phase 2 Outline
   - Alle H3 Unterpunkte abdecken
   - ~200-300 Wörter für ganzen H2
   - Content ONLY (kein HTML, kein Styling)
   - Markdown-Format:

```markdown
## H2 Titel

[Intro-Absatz zum H2, 2-3 Sätze]

### H3 Unterpunkt 1

[Content für H3, mit Beispielen/Details]

- Liste-Punkt 1
- Liste-Punkt 2
- Liste-Punkt 3

### H3 Unterpunkt 2

[Weiterer Content]

**Info-Box Konzept:** [Wichtiger Hinweis/Tipp - wird später formatiert]

### H3 Unterpunkt 3 (falls vorhanden)

[Finale Details]
```

4. Zeige Entwurf:
```
Hier ist H2 '[Titel]':

[kompletter H2 Entwurf]

---

OK? Oder Feedback: [änderung]
```

5. User-Antwort:
   - "OK" → Weiter zu nächstem H2
   - "Feedback: ..." → Revisieren, H2 neu schreiben
   - Repeat bis User zufrieden ist

6. **AKTUALISIERE `.md` Datei:**
   - Ersetze Platzhalter `(wird noch geschrieben)` mit finalem H2 Content
   - Speichere `.md`

7. **REPEAT für alle H2s aus Phase 2 Outline**

---

### Schritt 5.5: Research-Feedback-Loop (OPTIONAL - Nach jedem H2)

**NACH H2-Entwurf (nach Schritt 5.4):**

**Die KI MUSS FOLGENDES fragen:**

```
Hier ist H2 '[Titel]':

[kompletter H2 Entwurf]

---

Vier Optionen:
1. "OK" → Weiter zu nächstem H2
2. "Feedback: [änderung]" → Überarbeite diesen H2
3. "Recherchiere Quellen" → WebFetch Quellen für diesen H2 durchführen
4. "Nur H3 X recherchieren" → WebFetch nur für spezifischen H3-Punkt
```

**Falls User "Recherchiere Quellen" antwortet:**

1. **Phase 1-2 Quellen prüfen:**
   - Schaue in Phase 1-2 Daten ob relevante Quellen bereits vorhanden sind
   - Falls ausreichend: Nutze diese direkt

2. **Falls nicht ausreichend → WebFetch neue Quellen:**

   Nutze die Quellen-Richtlinien aus Phase 1 (primär: ResearchGate, Google Scholar, Fachjournale):

   ```
   WebFetch durchführen für diesen H2:

   Query: "[H2-Thema/H3-Punkt] + spezifisches Claim/Statistik"
   Portale durchsuchen:
   - ResearchGate.net: [Query]
   - Google Scholar: scholar.google.com [Query]
   - [Topic-spezifische Fachjournale]

   Für jede gefundene Quelle:
   URL: [source_url]
   Prompt: "Extrahiere für '[H2-Punkt]':
   - Hauptaussage/Erkenntnis
   - Relevante Statistiken/Daten
   - Expert-Zitate
   - Publikationsjahr & Autoren"
   ```

3. **Quellen in H2 einbauen (Markdown-Format):**

   ```markdown
   Dies ist ein wichtiger Punkt [laut dieser ResearchGate-Studie](https://...)
   und zeigt...

   Experten sagen: "Zitat hier" [Quelle: Autor et al., 2024](https://...)
   ```

4. **Überarbeiteter H2 mit Quellen zeigen:**

   ```
   Ich habe diese Quellen hinzugefügt:
   - [ResearchGate: "Studie-Titel"](URL)
   - [Google Scholar: "Paper-Titel"](URL)

   Hier ist der überarbeitete H2:
   [Updated H2 mit Quellen]

   ---

   OK? Oder noch weitere Anpassungen?
   ```

5. **Rückkehr zu Feedback-Loop:**
   - User kann wieder "OK", "Feedback", oder "Mehr Quellen" antworten
   - Repeat bis User zufrieden ist
   - Dann Schritt 7: **REPEAT für alle H2s aus Phase 2 Outline**

---

### Schritt 6: "Kurz zusammengefasst" Box erstellen (AM ENDE)

**NACHDEM alle H2s fertig sind:**

**Die KI MUSS FOLGENDES TUN:**

1. Extrahiere die 3-4 **Kernpunkte** aus allen H2s:
   - Meist: erste Sätze jedes H2s
   - Oder: die "Erinnerungen" aus Info-Boxen

2. Schreibe Box:

```markdown
## Kurz zusammengefasst:

- Kernpunkt 1: [kurz zusammengefasst]
- Kernpunkt 2: [kurz zusammengefasst]
- Kernpunkt 3: [kurz zusammengefasst]
- Kernpunkt 4: [optional]

**Info-Box Konzept:** (wird später formatiert als styled Box)
```

3. **EINFÜGEN in `.md`:**
   - Position: NACH Einleitung (vor ersten H2)
   - Format: Markdown List
   - Später wird das formatiert mit HTML Styling

4. Zeige User:
```
Hier ist die "Kurz zusammengefasst" Box:

[Box Content]

OK?
```

---

### Schritt 7: FAQ schreiben (NACH allen H2s + Box)

**Die KI MUSS FOLGENDES TUN:**

1. Generiere 3-5 häufige Fragen basierend auf:
   - Phase 2 Outline (Falls FAQ-Sektion geplant)
   - Oder selbstständig Longtail-Fragen zum Keyword generieren

2. Schreibe FAQ in Markdown:

```markdown
## Häufige Fragen (FAQ)

### Frage 1?
[Kurze, konkrete Antwort, 2-3 Sätze]

### Frage 2?
[Antwort]

### Frage 3?
[Antwort]

### Frage 4?
[Antwort, falls gewünscht]

### Frage 5?
[Antwort, falls gewünscht]
```

3. Frage User:
```
Passt die FAQ so? Weitere Fragen hinzufügen? Oder entfernen?
```

4. User-Antwort:
   - "OK" → Weiter zu Schritt 8
   - "Feedback: ..." → Revisieren

5. **AKTUALISIERE `.md`:** Füge FAQ am Ende ein

---

### Schritt 8: Fazit schreiben (FINAL)

**Die KI MUSS FOLGENDES TUN:**

1. Schreibe Fazit/Zusammenfassung:
   - 100-150 Wörter
   - Bezug zum H1 Title
   - Call-to-Action (optional: "Versuch es selbst!", "Teile deine Erfahrung", etc.)
   - Conversational, Du-Form

```markdown
## Fazit

[Zusammenfassung der wichtigsten Punkte]

[Call-to-Action oder Ermutigung]
```

2. Frage User:
```
Passt das Fazit?
```

3. **AKTUALISIERE `.md`:** Fazit am Ende einfügen

---

### Schritt 9: Kompletten Artikel in `.md` finalisieren

**Die KI MUSS FOLGENDES TUN:**

1. Lese komplette `.md` aus `/articles/working/[project_uuid].md`

2. Prüfe Struktur:
   - H1 Titel vorhanden?
   - Einleitung nach H1?
   - "Kurz zusammengefasst" nach Einleitung?
   - Alle H2s vorhanden?
   - FAQ vorhanden?
   - Fazit am Ende?

3. Zeige User Inhaltsverzeichnis:
```
✅ Kompletter Artikel:

1. H1: [Titel]
2. Einleitung
3. Kurz zusammengefasst
4. H2 1: [Titel]
5. H2 2: [Titel]
... (alle Sections auflisten)
6. FAQ
7. Fazit

Wort-Count: ~[ZAHL] Wörter (Ziel: 1.500-2.000)

Bereit für Phase 4 (Validierung)?
```

---

### Schritt 10: Artikel finalisieren

**Tool:** Lokale Write

**Die KI MUSS FOLGENDES TUN:**

1. Stelle sicher dass komplettes Markdown in `/Articles/[keyword-slug]/content/content.md` gespeichert ist

2. **Zeige Erfolgs-Meldung:**
```
✅ Phase 3 abgeschlossen!
- Content-Markdown in `/Articles/[keyword-slug]/content/content.md` gespeichert
- Phase Status: 'completed'
- Wort-Count: ~[ZAHL] Wörter (Ziel: 1.500-2.000)

Nächster Schritt: Phase 4 (Validierung & Formatierung)
Bereit zu starten? (J/N)
```

---

## Quellen-Richtlinien für Content-Writer (Phase 3)

### Wann Quellen notwendig sind:

- ✅ **Statistiken/Zahlen/Daten-Claims:** "87% der User...", "Studien zeigen..."
- ✅ **Wissenschaftliche Erkenntnisse:** "Basierend auf ResearchGate-Studie..."
- ✅ **Expert-Zitate:** "Laut Experte XY...", "Forscher sagen..."
- ✅ **Methoden/Best Practices mit Urheberschaft:** "Die ABC-Methode [Quelle]..."
- ❌ **Allgemeines Wissen:** Keine Quelle nötig
- ❌ **Offensichtliche Fakten:** Keine Quelle nötig

### Quellen-Qualität:

1. **Primär (höchste Qualität - nutzen wenn möglich):**
   - ResearchGate.net
   - Google Scholar (scholar.google.com)
   - Fachjournale & Uni-Publikationen
   - Offizielle Studien & Research Papers

2. **Sekundär (falls primär nicht verfügbar):**
   - Hochwertige Expertenartikel mit Quellenangabe
   - Whitepapers von anerkannten Instituten
   - Behördliche/offizielle Quellen

3. **NICHT verwenden:**
   - ❌ Unverified Blogs ohne Quellenangabe
   - ❌ Social Media Posts ohne Quelle
   - ❌ Veraltete Quellen (>5 Jahre, außer klassische Fachliteratur)

### Quellen-Format (Markdown in Phase 3):

```markdown
Dies ist ein wichtiger Punkt [laut dieser ResearchGate-Studie](https://researchgate.net/...)
und zeigt...

Experten sagen: "Zitat hier" [Quelle: Autor et al., 2024](https://scholar.google.com/...)
```

**Wichtig für Phase 4 HTML-Konvertierung:**
- Alle Links werden automatisch mit `target="_blank"` konvertiert
- Leser öffnen Quellen in neuem Tab, verlassen den Artikel nicht

---

## Markdown-Format Referenz (Phase 3)

```markdown
# [H1 Titel]

[Einleitung 100-150 Wörter, Du-Form, conversational]

## Kurz zusammengefasst:

- Punkt 1
- Punkt 2
- Punkt 3

---

## H2 Titel 1

[Intro zum H2, 2-3 Sätze]

### H3 Unterpunkt 1

[Content, 50-100 Wörter]

- Liste-Punkt 1
- Liste-Punkt 2

### H3 Unterpunkt 2

[Content]

**Info-Box Konzept:** [Text für Info-Box, wird später formatiert]

---

## H2 Titel 2

[Struktur wiederholt]

---

## Häufige Fragen (FAQ)

### Frage 1?

[Kurze Antwort, 2-3 Sätze]

### Frage 2?

[Antwort]

---

## Fazit

[Zusammenfassung + CTA, 100-150 Wörter]
```

---
