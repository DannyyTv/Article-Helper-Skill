# Content Design Guide – Agent-Anleitung

Dieser Guide dokumentiert Best Practices für hervorragendes Content Design in Blog-Artikeln. Agent nutzt diese zur Erstellung von dynamischen, hochperformanten Artikeln.

---

## 1. H2-LAYOUT VARIATION (Anti-Monotonie)

Jeder H2 muss eine ANDERE Struktur haben. Agent erkennt den Typ anhand des Contents:

### H2 Struktur-Typen:

**DEFINITION FORMAT** – Für Fachbegriffe, Konzepte
- Intro-Absatz (2-3 Sätze)
- Prägnante Definition (40-60 Wörter, direkte Antwort)
- Expandierter Kontext (weitere Absätze mit Details)
- Beispiel: "Was ist die Pomodoro-Technik?"

**LIST FORMAT** – Für Aufzählungen, Best Practices, Tipps
- Intro-Absatz
- Nummerierte oder Bullet-Liste (3-5 Punkte)
- Zusammenfassung oder praktischer Tipp
- Beispiel: "Die 5 besten Pomodoro-Strategien"

**COMPARISON FORMAT** – Für Pro/Contra, Alternativen, Vergleiche
- Intro-Absatz
- Vergleichs-Tabelle oder Pro/Contra-Liste
- Schlussfolgerung/Empfehlung
- Beispiel: "Pomodoro vs. andere Zeitmanagement-Methoden"

**QUOTE/INSIGHT FORMAT** – Für wichtige Erkenntnisse, Experten-Aussagen
- Intro-Absatz
- Zitat oder Key Insight (separates Blockquote-Design)
- Erklärung/Kontext der Aussage
- Praktische Anwendung
- Beispiel: "Was Produktivitäts-Experten über Fokus sagen"

**STEP-BY-STEP FORMAT** – Für How-To, Prozesse, Anleitungen
- Intro-Absatz
- Nummerierte Steps (1, 2, 3...) mit Details
- Resultat/Outcome/Tipps
- Beispiel: "Wie man die Pomodoro-Technik startet"

### Agent-Aktion:
Vor dem Schreiben jedes H2 fragen: **"Was ist der Content-Typ?"**
- Definition? → Definitional Format
- Anleitung/Wie-man? → Step-by-Step Format
- Pro/Contra? → Comparison Format
- Wichtige Erkenntnisse? → Quote/Insight Format
- Liste wichtig? → List Format

**Regel:** Keinen H2 wiederholt mit gleicher Struktur verwenden.

---

## 2. FEATURED SNIPPET OPTIMIERUNG

Erste Antwort ist PRÄGNANT (40-60 Wörter), DANN Details. Dies hilft Google, für Position Zero zu ranken.

### Struktur:

```
Erkannte Frage (H2-Titel): "Was ist die Pomodoro-Technik?"

Prägnante Antwort (ZUERST):
"Die Pomodoro-Technik ist eine Zeitmanagement-Methode,
die Arbeit in 25-Minuten-Fokus-Blöcke unterteilt,
unterbrochen durch 5-Minuten-Pausen. Dies steigert Konzentration
und verhindert Burnout durch rhythmische Arbeitszyklen."

DANN weitere Details:
[Absätze mit Erklärungen, Beispielen, Kontext]
```

### Agent-Aktion:
1. H2-Frage erkennen
2. 40-60 Wörter direkte, vollständige Antwort schreiben
3. DANN expandieren mit Details/Kontext

---

## 3. INFO-BOX VARIATION (Ohne Icons)

Nicht alle Info-Boxen sind gleich. Agent variiert den Typ je nach Content:

### Info-Box Typen:

**PRO-TIPP-BOX:**
```html
<div style="background-color: #f8f9fa; padding: 20px;
border-left: 4px solid #DD4067; border-radius: 8px; margin: 20px 0;">
<p><strong>Pro-Tipp:</strong> [Praktischer Hinweis für schnellen Erfolg]</p>
</div>
```
Wann: Praktische Shortcuts, Effizienz-Tipps, Hacks

**WARNING-BOX:**
```html
<div style="background-color: #f8f9fa; padding: 20px;
border-left: 4px solid #DD4067; border-radius: 8px; margin: 20px 0;">
<p><strong>Wichtig:</strong> [Häufiger Fehler oder Warnung]</p>
</div>
```
Wann: Zu vermeidende Fehler, kritische Hinweise, Fallstricke

**DEFINITION-BOX:**
```html
<div style="background-color: #f8f9fa; padding: 20px;
border-left: 4px solid #DD4067; border-radius: 8px; margin: 20px 0;">
<p><strong>Definition:</strong> [Kurze präzise Erklärung]</p>
</div>
```
Wann: Fachbegriffe erklären, Konzepte definieren, Verwirrung klären

**BEST PRACTICE-BOX:**
```html
<div style="background-color: #f8f9fa; padding: 20px;
border-left: 4px solid #DD4067; border-radius: 8px; margin: 20px 0;">
<p><strong>Best Practice:</strong> [Bewährter, empfohlener Ansatz]</p>
</div>
```
Wann: Industry Standards, bewährte Methoden, Professionelle Ansätze

### Agent-Aktion:
Während Content-Erstellung: "Braucht dieser H2 eine Info-Box? Welcher Typ?"
- Praktischer Hinweis? → Pro-Tipp
- Häufiger Fehler? → Warning
- Unbekannter Begriff? → Definition
- Empfohlene Methode? → Best Practice

**Variation:** Pro H2 maximal 1 Info-Box. Nicht jeden H2 mit Box füllen.

---

## 4. TABELLEN & STRUKTURIERTE DATEN

### Wann Tabelle verwenden:

- Pro/Contra Vergleich (2+ Spalten)
- Datenvergleich (Tool A vs Tool B vs Tool C)
- Attribut-Übersicht (Eigenschaft 1, 2, 3...)
- Vergleichende Kriterien

### HTML Format:

```html
<table style="width: 100%; border-collapse: collapse;">
  <thead>
    <tr style="background-color: #f8f9fa;">
      <th style="border: 1px solid #ddd; padding: 10px; text-align: left;"><strong>Kriterium</strong></th>
      <th style="border: 1px solid #ddd; padding: 10px; text-align: left;"><strong>Option A</strong></th>
      <th style="border: 1px solid #ddd; padding: 10px; text-align: left;"><strong>Option B</strong></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="border: 1px solid #ddd; padding: 10px;">Preis</td>
      <td style="border: 1px solid #ddd; padding: 10px;">$10/Monat</td>
      <td style="border: 1px solid #ddd; padding: 10px;">$20/Monat</td>
    </tr>
    <tr style="background-color: #f8f9fa;">
      <td style="border: 1px solid #ddd; padding: 10px;">Geschwindigkeit</td>
      <td style="border: 1px solid #ddd; padding: 10px;">Langsam</td>
      <td style="border: 1px solid #ddd; padding: 10px;">Schnell</td>
    </tr>
  </tbody>
</table>
```

### Wann Liste verwenden:

- Einfache Aufzählungen ohne Vergleich
- Step-by-Step Anleitungen
- Best Practices ohne Kontrastierung
- Linear, keine Dimensionen nötig

### Agent-Aktion:
Vor jedem H2: "Braucht dieser Abschnitt Datenvergleich?"
- Ja, 2+ Spalten nötig? → Tabelle
- Nein, einfache Aufzählung? → Liste

---

## 5. ZITATE & TESTIMONIALS

Zitate sollten VISUELL und STRUKTURELL unterschieden sein von normalem Text.

### Blockquote Format:

```html
<blockquote style="border-left: 4px solid #DD4067;
padding-left: 15px; margin-left: 0; font-style: italic;
color: #555;">
"Das ist ein prägnantes Experten-Zitat zum Thema,
das eine wichtige Erkenntnis zusammenfasst."
<br/><strong>— Experten-Name, Titel/Quelle, Jahr</strong>
</blockquote>
```

### Inline-Zitat Format (für kurze Quotes):

```html
<p>Nach dem Experten <a href="..." target="_blank">XY</a> ist der beste Ansatz:
"kurzes Zitat hier". Dies zeigt...</p>
```

### Agent-Aktion:
- Zitate sollten in jedem 3-4. H2 vorkommen (nicht in allen!)
- Blockquote für Haupt-Zitate (längere Aussagen)
- Inline-Zitat für Unterstützungs-Zitate (kurz, nebenbei)
- IMMER Quelle angeben (Experte, Publikation, Jahr)

---

## 6. LINK-HANDLING & INLINE REFERENCES

### Regel 1: Alle EXTERNEN Links im NEUEN TAB

```html
❌ FALSCH: <a href="https://example.com">Link</a>

✅ RICHTIG: <a href="https://example.com" target="_blank" rel="noopener noreferrer">Link</a>
```

### Regel 2: Inline Links – NUR wo Kontext sinnvoll

Links gehören nicht überall, sondern **nur wo kontextuell relevant:**

**SZENARIO 1: Fachbegriff wird im Artikel erklärt**
```
❌ FALSCH: "Die [Pomodoro-Technik verlinkt] ist eine Methode..."
(Redundant – Begriff wird ohnehin erklärt)

✅ RICHTIG: "Die Pomodoro-Technik ist eine Methode,
die 25-Minuten-Fokus-Blöcke nutzt..."
(Keine Link nötig, wird im Artikel ausführlich erklärt)
```

**SZENARIO 2: Externe Quelle/Studie referenzieren**
```
✅ RICHTIG: "Nach einer Studie von [Forscher Name, verlinkt]
zeigt sich, dass 25-Minuten-Intervalle optimal sind."
(Link unterstützt Glaubwürdigkeit mit Quelle)
```

**SZENARIO 3: Tool/Service als Best Practice erwähnen**
```
✅ RICHTIG: "Viele nutzen Apps wie [Tool-Name, verlinkt]
um die Timer-Funktion zu automatisieren."
(Link hilft Leser direkt weiterhelfen)
```

**SZENARIO 4: Weiterführender verwandter Content (interne Links)**
```
✅ RICHTIG: "Falls du mehr über [verwandtes Thema, verlinkt]
erfahren möchtest, haben wir einen ausführlichen Guide dazu."
(Link zu thematisch verwandtem Artikel)
```

### Anchor-Text Best Practices:

- **Kurz:** Max 5 Wörter
- **Relevant:** Beschreibt Ziel-Seite
- **Natürlich:** "Diese Studie" statt "klick hier"
- **Semantisch:** "Pomodoro-Apps" statt "best productivity tools"

### Agent-Aktion bei Link-Platzierung:

1. **Ist der Link notwendig für Verständnis?**
   - Nein → nicht verlinken
   - Ja → Inline-Link setzen

2. **Passt Kontext des Links zur Stelle?**
   - Nein → woanders setzen oder streichen
   - Ja → platzieren

3. **Anchor-Text max 5 Wörter?**
   - Nein → kürzen
   - Ja → verwenden

4. **Externe Links?** → `target="_blank" rel="noopener noreferrer"`

5. **Link-Anzahl pro H2:** Maximal 2-3 Links (200-300 Wörter)

6. **Gesamt-Artikel:** 5-8 Links optimal, nicht mehr als 1 Link pro 100 Wörter

---

## 7. KEYWORD-OPTIMIERUNG (SMART, NICHT STUFFING)

### Kernregel: Keywords natürlich integrieren, NICHT erzwingen

Keyword-Dichte sollte 2-5% sein, aber nicht gezielt angestrebt – natürliche Platzierung ist wichtiger.

### Wo Keywords gehören (NATÜRLICH):

| Element | Placement | Beispiel |
|---------|-----------|----------|
| **H1-Titel** | Primäres Keyword + Nutzen | "Pomodoro-Technik: Fokus für mehr Produktivität" |
| **Erster Satz** | Keyword 1x, casual eingebaut | "Die Pomodoro-Technik hilft dir, dich 25 Minuten..." |
| **H2-Titel** | Sekundäre Keywords, Variationen | "Wie die Pomodoro-Methode funktioniert" (Variation) |
| **H3-Titel** | Longtail Varianten | "Best Pomodoro-Apps für Anfänger" |
| **Alt-Text (Bilder)** | Beschreibung + Keyword falls relevant | alt="Pomodoro-Timer mit 25-Minuten-Intervall" |
| **Anker-Text (Links)** | Kurz, relevant, natürlich | Link: "diese Pomodoro-Studie" |

### Beispiel (RICHTIG):

```
H1: "Pomodoro-Technik: Fokus-Blöcke für mehr Produktivität"
    └─ Primäres Keyword: "Pomodoro-Technik"

Erster Satz: "Die Pomodoro-Technik ist eine bewährte Zeitmanagement-Methode,
die dir hilft, dich 25 Minuten lang vollständig zu konzentrieren."
    └─ Keyword 1x, natürlich, nicht wiederholt

H2-1: "Wie die Pomodoro-Methode funktioniert"
    └─ Variation: "Pomodoro-Methode" statt "Pomodoro-Technik"

H2-2: "Warum Fokus-Blöcke deine Produktivität steigern"
    └─ Andere Variation: "Fokus-Blöcke" + "Produktivität"

H2-3: "Die beste Pomodoro-App für zeitgesteuerte Sessions"
    └─ Longtail: "Pomodoro-App"
```

### Beispiel (FALSCH – Keyword Stuffing):

```
"Die Pomodoro-Technik, auch als Pomodoro-Methode bekannt, ist eine
Pomodoro-Technik für die Pomodoro-Zeitmanagement. Die Pomodoro-Technik
nutzt Pomodoro-Timer..."
    → Unlesbar, repetitiv, Google penaliert
```

### Agent-Aktion bei Keyword-Integration:

1. **Keyword im H1 und ersten Absatz** (je 1x, natürlich)
2. **Sekundäre Keywords in H2-Titeln variieren** (Synonyme, Variationen)
3. **Longtail Keywords in H3-Titeln**
4. **Test: Laut vorlesen** – klingt es natürlich? Wenn nein → umschreiben
5. **Keyword-Dichte überprüfen:** (Keyword Vorkommen / Gesamt-Wörter) × 100 = sollte 2-5% sein
6. **Keine erzwungene Wiederholung** – wenn natürlich, 1-2x pro 500 Wörter

---

## 8. FAQ-STRUKTUR (Keine Wiederholungen)

FAQ sollte Search-Queries und Longtail-Fragen abdecken, NICHT H2-Zusammenfassungen wiederholen.

### Struktur:

```html
<h2>Häufig gestellte Fragen (FAQ)</h2>

<div class="faq-accordion">
  <details>
    <summary><strong>Wie lange sollte eine Pomodoro-Session sein?</strong></summary>
    <p>Die klassische Pomodoro-Session dauert 25 Minuten Fokus-Zeit.
    Einige Anfänger starten mit 15 Minuten, erfahrene Nutzer arbeiten
    mit bis zu 50 Minuten. Wichtig ist: Finde deinen persönlichen Rhythmus.</p>
  </details>

  <details>
    <summary><strong>Kann ich die Pomodoro-Technik für Remote-Arbeit nutzen?</strong></summary>
    <p>Ja, besonders effektiv. Die Technik ist unabhängig vom Arbeitsort.
    Im Home-Office hilft sie sogar, Pausen einzuhalten und
    Ablenkungen zu minimieren.</p>
  </details>
</div>
```

### FAQ-Richtlinien:

- **3-5 Fragen** pro Artikel
- **Longtail Variationen:** "Wie...", "Kann...", "Wann...", "Wo...", "Welche..."
- **Nicht repetitiv:** Keine Frage wie "Was ist die Pomodoro-Technik?" (= H1/Einleitung)
- **Konkrete Antworten:** Max 3 Sätze, direkt und hilfreich
- **Suchquery-fokussiert:** Fragen sind real von Nutzern gesucht

### Agent-Aktion:

Vor FAQ-Schreiben:
1. **Deckungsanalyse:** Welche Search-Queries sind NICHT in H2s beantwortet?
2. **Longtail-Variationen:** "Wie...", "Kann...", "Wo..." Fragen generieren
3. **Wiederholungs-Check:** Keine Frage sollte H2-Inhalte 1:1 wiederholen
4. **Kurz & praktisch:** Antwort max 3 Sätze, sehr konkret

---

## 9. FAZIT-STRUKTUR (Keine Wiederholung)

Fazit hat 3-Teil-Struktur: Mindset + konkrete Steps + CTA (inspirierend, nicht aufdringlich).

### Struktur:

```html
<h2>Fazit</h2>

<p><strong>Der wichtigste Mindset-Shift:</strong>
Konsistenz über Perfektion. Die Pomodoro-Technik funktioniert nicht
durch einsame Marathon-Sessions, sondern durch tägliche, rhythmische Arbeit.</p>

<p><strong>Konkrete nächste Schritte:</strong></p>
<ul>
<li><strong>Diese Woche starten:</strong> Eine 25-Minuten-Session morgen, beobachte wie dein Fokus sich verbessert.</li>
<li><strong>Rhythmus finden:</strong> Nach 3-4 Sessions weißt du, ob 25 Minuten für dich passen.</li>
<li><strong>Pausen optimieren:</strong> Nutze die 5-Minuten-Pause für echte Erholung, nicht Handy.</li>
<li><strong>Erfolg tracken:</strong> Notiere wie viele Pomodoros du pro Tag schaffst.</li>
</ul>

<p>Die Pomodoro-Technik ist kein Geheimrezept, sondern ein einfaches,
bewährtes System. Tausende Nutzer berichten: Mit dieser einen Technik
haben sie ihre Produktivität verdoppelt. Probiere sie diese Woche aus
und beobachte selbst, was sich verändert.</p>
```

### Fazit-Richtlinien:

- **NICHT:** H2-Zusammenfassungen repetieren
- **JA:** Ein neuer Mindset-Insight (1 Satz, prägnant)
- **JA:** 3-4 konkrete, actionable nächste Schritte
- **JA:** CTA inspirierend, nicht verkäufig
- **Länge:** 100-150 Wörter

### ❌ Zu vermeiden:

```
"Wir haben gelernt, dass die Pomodoro-Technik wichtig ist
und dass Fokus-Blöcke dir helfen..."
→ Repetiert H1/Einleitung
```

---

## QUICK REFERENCE (Agent-Checkliste)

| Phase | Aktion | Beispiel |
|-------|--------|---------|
| **Content-Typ wählen** | Welcher H2-Typ? | Definition, List, Comparison, Quote, Step-by-Step |
| **Erste Antwort** | 40-60 Wörter prägnant | "Die Pomodoro-Technik ist..." (dann Details) |
| **H2-Struktur variieren** | Nicht wiederholt | H2-1: Definition, H2-2: List, H2-3: Comparison |
| **Info-Box Typ** | Pro-Tipp, Warning, Definition, Best Practice | Nicht jeder H2 braucht Box |
| **Tabelle vs. Liste** | Vergleich 2+ Spalten? | Ja → Tabelle, Nein → Liste |
| **Zitate nutzen** | Alle 3-4. H2, Blockquote | Mit Quelle (Experte, Jahr) |
| **Links setzen** | Nur wo sinnvoll, max 2-3 pro H2 | Externe = `target="_blank"` |
| **Keywords einbauen** | 1x H1, 1x erster Satz, Variationen in H2/H3 | Keine Wiederholung, laut vorlesen |
| **FAQ füllen** | Longtail-Variationen, nicht H2-Wiederholungen | 3-5 Fragen, konkrete Antworten |
| **Fazit schreiben** | Mindset + Steps + CTA | Nicht repetitiv, inspirierend |

---

**Version:** 1.0
**Zielgruppe:** AI Agents für Content-Erstellung
**Prinzip:** Prägnant, actionable, Agent-verständlich
