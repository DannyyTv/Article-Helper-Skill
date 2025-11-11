# Phase 4: Validierung & HTML-Formatierung

## Zweck

Diese Phase **validiert** den Artikel gegen strikte Qualitätskriterien (Wort-Count, Struktur, Tonalität, Content-Qualität) UND **formatiert ihn gleichzeitig zu HTML** mit allen Design-Elementen (Farben, Abstände, Info-Boxen, FAQ-Accordion). Der Agent arbeitet **abschnittweise** (H2 für H2): Validierung + HTML-Umwandlung zusammen.

**OUTPUT:** `/Articles/[keyword-slug]/validation/validation.md`

---

## Tools in Phase 4

**Die KI nutzt FOLGENDE Tools in dieser Phase:**

| Schritt | Tool | Funktion | Optional |
|---------|------|----------|----------|
| 1 | Read (lokal) | Markdown-Artikel laden (`/Articles/[keyword-slug]/content/`) | Nein |
| 2 | Claude (intern) | Struktur analysieren + Templates laden | Nein |
| 3+ | Claude (intern) | Validierung + HTML-Conversion pro Abschnitt | Nein |
| Final | Write (lokal) | Finales Markdown+HTML in `.md` schreiben | Nein |

**Obligatorisch:** Lokale Read/Write, Template-Referenzierung

---

## ⚡ WICHTIG: Konkrete KI-Aktionen

1. **LESE `../content-design-guide.md`** für Content Design Standards
2. Markdown-Artikel aus `/Articles/[keyword-slug]/content/content.md` laden
3. **ABSCHNITTWEISE** validieren + zu HTML konvertieren (H1 → Einleitung → Box → H2s → FAQ → Fazit)
4. HTML-Templates referenzieren
5. HTML am Ende der `.md` Datei unter `## 🔧 HTML-REFERENZ` hinzufügen
6. User-Feedback nach jedem Abschnitt einholen
7. Finales Markdown+HTML lokal speichern in `/Articles/[keyword-slug]/validation/validation.md`
8. **Ergebnis MUSS persistent lokal sein vor Session-Ende**

---

## Validierungs-Kriterien

**Wort-Count:**
- Gesamt: 1.500-2.000 | Pro H2: 200-300 | Einleitung: 100-150 | Fazit: 100-150 | FAQ: 3-5 Fragen

**Struktur:**
- 1x H1 | Einleitung → Box → H2s (mit H3s) | FAQ Accordion | Fazit | Abstände zwischen Abschnitten

**Tonalität:**
- Du-Form konsistent | Conversational | Kurze Absätze (max 4 Sätze) | Aktive Verben | Keine akademische Sprache

**Content:**
- Konkrete Beispiele | Actionable Tipps | Kein Jargon ohne Erklärung | Keyword in H1 + Einleitung


## Verzeichnis-Struktur

```
/Articles/[keyword-slug]/
├── content/content.md (Markdown aus Phase 3)
└── validation/validation.md (HTML aus Phase 4 - wird in Phase 4 erstellt)
```

**Hinweis:** `validation.md` enthält das fertige HTML (kein Markdown), direkt am Anfang für Phase 5 (WordPress Upload).

---

## Workflow

### Schritt 1: Artikel laden & Kontext vorbereiten

**Die KI MUSS FOLGENDES TUN:**

1. Frage User nach `keyword-slug` (oder verwende aktive Session)
2. Lese Markdown-Artikel aus `/Articles/[keyword-slug]/content/content.md`

3. Parse die Struktur:
   - H1 Titel extrahieren
   - Einleitung, H2s, FAQ, Fazit identifizieren
   - Wort-Count berechnen

4. Zeige User Übersicht:
```
📋 Phase 4: Validierung & HTML-Formatierung

**Projekt:** [Titel]
**Aktueller Wort-Count:** [ZAHL] Wörter (Ziel: 1.500-2.000)
**Struktur:** 1 Einleitung + 1 Kurz-zusammengefasst-Box + [X] H2s + FAQ + Fazit

Templates geladen:
- article-structure.html
- info-box.html
- spacing.html
- faq-accordion.html

Starten wir mit der Validierung?
(1. H1 + Einleitung → 2. Kurz zusammengefasst Box → 3. H2 Abschnitte → 4. FAQ → 5. Fazit)
```

---

### Schritt 2: H1 + Einleitung validieren & konvertieren

**Validierung:**
- H1 Länge: 55-60 Zeichen, Keyword + Nutzen vorhanden?
- Einleitung: 100-150 Wörter, Du-Form konsistent, Hook vorhanden?

Falls Fehler: User fragen "Sollen wir anpassen?" → Markdown überarbeiten oder mit Warnung weitermachen

**HTML-Konvertierung:**
```html
<h1>[Titel]</h1>
<p>[Einleitung]</p>
```

Speichern in `.md` unter `## 🔧 HTML-REFERENZ` (wird in Schritt 8 zusammengefasst)

---

### Schritt 3: "Kurz zusammengefasst" Box validieren & konvertieren

**Validierung:**
- 3-4 Punkte, jeder kurz (max 2 Sätze), kein Jargon ohne Erklärung

Falls Fehler: User fragen "Box anpassen?" → Markdown überarbeiten oder weitermachen

**HTML-Konvertierung:**
Template: `templates/info-box.html`
```html
<div style="background-color: #f8f9fa; padding: 20px; border-left: 4px solid #DD4067; border-radius: 8px; margin: 20px 0;">
<p><strong>Kurz zusammengefasst:</strong></p>
<ul><li>[Punkt 1]</li><li>[Punkt 2]</li></ul>
</div>
<div style="height:100px" aria-hidden="true"></div>
```

Speichern in `.md` unter `## 🔧 HTML-REFERENZ`

---

### Schritt 4: H2 Abschnitte validieren & konvertieren (ITERATIV)

**FÜR JEDEN H2:**

**Validierung:**
- Wort-Count: 200-300? | Alle H3 vorhanden? | Konkrete Beispiele? | Max 4 Sätze pro Absatz? | Du-Form? | Keine Füllwörter?

Falls Fehler: User fragen "Überarbeiten?" → Markdown aktualisieren oder weitermachen

**HTML-Konvertierung:**
Template: `templates/article-structure.html`
```html
<h2>[Titel]</h2>
<p>[Intro]</p>
<div style="height:50px" aria-hidden="true"></div>
<h3>[H3 Punkt]</h3>
<p>[Content, max 4 Sätze]</p>
<ul><li><strong>[Punkt]:</strong> [Erklärung]</li></ul>
<div style="height:30px" aria-hidden="true"></div>
<!-- Info-Boxen falls vorhanden -->
<div style="background-color: #f8f9fa; padding: 20px; border-left: 4px solid #DD4067; border-radius: 8px;">
<p><strong>[Titel]:</strong> [Inhalt]</p>
</div>
<div style="height:100px" aria-hidden="true"></div>
```

Speichern in `.md` unter `## 🔧 HTML-REFERENZ` + wiederholen für jeden H2

---

### Schritt 5: FAQ validieren & konvertieren

**Validierung:**
- 3-5 Fragen, konkret (wie/warum/kann/wann), Antworten max 3 Sätze, Longtail-Keywords?

Falls Fehler: User fragen "FAQ anpassen?" → Markdown überarbeiten oder weitermachen

**HTML-Konvertierung:**
Template: `templates/faq-accordion.html`
```html
<h2>Häufige Fragen (FAQ)</h2>
<div class="faq-accordion">
  <details>
    <summary><strong>[Frage 1]?</strong></summary>
    <p>[Antwort 1]</p>
  </details>
  <details>
    <summary><strong>[Frage 2]?</strong></summary>
    <p>[Antwort 2]</p>
  </details>
</div>
<div style="height:100px" aria-hidden="true"></div>
```

Speichern in `.md` unter `## 🔧 HTML-REFERENZ`

---

### Schritt 6: Fazit validieren & konvertieren

**Validierung:**
- Wort-Count: 100-150? | Zusammenfassung TOP Punkte? | Call-to-Action vorhanden? | Du-Form?

Falls Fehler: User fragen "Fazit anpassen?" → Markdown überarbeiten oder weitermachen

**HTML-Konvertierung:**
```html
<h2>Fazit</h2>
<p>[Zusammenfassung der Hauptpunkte]</p>
<p>[Call-to-Action oder Ermutigung]</p>
```

Speichern in `.md` unter `## 🔧 HTML-REFERENZ`

---

### Schritt 7: Finalen Artikel prüfen

**Finale Struktur-Prüfung:**
- H1 → Einleitung → Box → H2s (mit H3s) → FAQ → Fazit
- Alle Abstände vorhanden (100px, 50px, 30px)
- Gesamtwort-Count: 1.500-2.000?

**Zeige User Zusammenfassung:**
```
✅ VALIDIERUNG ABGESCHLOSSEN!

Struktur: H1 | Einleitung | Box | [X] H2s | FAQ | Fazit
Wort-Count: [ZAHL] (OK wenn 1.500-2.000) ✅
Tonalität & Formatierung: ✅

Warnungen (falls vorhanden): [Liste]

Ready für Phase 5? (J/N)
```

---

### Schritt 8: Finalisierung & Speicherung

**Tool:** Lokale Write

1. Speichere komplettes HTML (nicht Markdown!) als neue `.md` Datei: `/Articles/[keyword-slug]/validation/validation.md`
   - Datei enthält NUR das HTML (kein Markdown, kein "HTML-REFERENZ" Label)
   - HTML ist sofort am Anfang, lesbar für WordPress Upload (Phase 5)

2. Zeige Erfolgs-Meldung:
```
✅ Phase 4 abgeschlossen!
- HTML gespeichert in `/Articles/[keyword-slug]/validation/validation.md`
- Ready für Phase 5? (J/N)
```

---

## User-Kommunikation

- **Start:** "Lade Markdown-Artikel..."
- **Übersicht:** "Wort-Count: [X], Struktur OK. Starten wir?"
- **H1/Einleitung:** "Validierung OK? Oder Feedback?"
- **H2-Schritt:** "Validieren wir H2 '[Titel]'?"
- **Fehler:** "⚠️ Überarbeiten? (J/N)"
- **Konvertierung:** "✅ HTML hinzugefügt"
- **Final:** "✅ Phase 4 fertig! Ready für Phase 5?"

---

## Template-Referenz

| Template | Zweck |
|----------|-------|
| `templates/article-structure.html` | H1/H2/H3/Listen/FAQ/Fazit Struktur |
| `templates/info-box.html` | Styled Info-Boxen & "Kurz zusammengefasst" |
| `templates/spacing.html` | Konsistente Abstände (100px/50px/30px) |
| `templates/faq-accordion.html` | FAQ mit `<details><summary>` |

---

## Wichtige Punkte

- **ABSCHNITTWEISE:** Validierung → HTML-Konvertierung (H1 → Einleitung → Box → H2s → FAQ → Fazit)
- **TEMPLATES:** Immer aus `/templates/` referenzieren
- **FARBEN:** `#DD4067` (Border), `#f8f9fa` (Background)
- **ABSTÄNDE:** 100px (H2-H2), 50px (H3-H3), 30px (vor/nach Boxen)
- **FINAL:** HTML am Ende der `.md` unter `## 🔧 HTML-REFERENZ` speichern
