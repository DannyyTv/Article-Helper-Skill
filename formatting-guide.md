# Websnapz Formatierungs-Referenz

Dieser Guide enthält alle HTML-Templates und CSS-Patterns für konsistente Artikel-Formatierung.

## HTML-Überschriften

```html
<h1>Haupttitel des Artikels</h1>
<h2>Hauptabschnitt</h2>
<h3>Unterabschnitt</h3>
```

**Regeln:**
- Nur EIN `<h1>` pro Artikel
- H2 für Hauptabschnitte (3-4 pro Artikel)
- H3 für Unterabschnitte innerhalb H2

## Info-Boxen

### Standard Info-Box
```html
<div style="background-color: #f8f9fa; padding: 20px; border-left: 4px solid #DD4067; border-radius: 8px; margin: 20px 0;">
<p><strong>Wichtiger Hinweis:</strong> Dein Text hier...</p>
</div>
```

**Abstands-Regel für Info-Boxen:**
- **VOR der Info-Box:** 30px Abstand hinzufügen (wenn Text davor)
  ```html
  <div style="height:30px" aria-hidden="true"></div>
  <div style="background-color: #f8f9fa; padding: 20px; border-left: 4px solid #DD4067; border-radius: 8px; margin: 20px 0;">
  ...
  </div>
  ```
- **NACH der Info-Box:** 30px Abstand hinzufügen (NUR wenn weiterer Content folgt)
  ```html
  <div style="background-color: #f8f9fa; padding: 20px; border-left: 4px solid #DD4067; border-radius: 8px; margin: 20px 0;">
  ...
  </div>
  <div style="height:30px" aria-hidden="true"></div>
  [Weiterer Content hier]
  ```
- **Ausnahme:** Wenn die Info-Box einen Abschnitt (H3) beendet, KEIN Abstand dahinter nötig

### Kurz zusammengefasst Box (am Artikel-Anfang)
```html
<div style="background-color: #f8f9fa; padding: 20px; border-left: 4px solid #DD4067; border-radius: 8px; margin: 20px 0;">
<p><strong>Kurz zusammengefasst:</strong></p>
<ul>
<li>Punkt 1</li>
<li>Punkt 2</li>
<li>Punkt 3</li>
</ul>
</div>
```

**KRITISCH:** Immer Farbe #DD4067 (Website-Highlight), NICHT #007cba (generisches Blau)

## Listen

### Einfache Liste
```html
<ul>
<li>Punkt 1</li>
<li>Punkt 2</li>
<li>Punkt 3</li>
</ul>
```

### Liste mit Hervorhebungen
```html
<ul>
<li><strong>Hauptpunkt:</strong> Erklärung dazu</li>
<li><strong>Zweiter Punkt:</strong> Weitere Details</li>
<li><strong>Dritter Punkt:</strong> Zusätzliche Info</li>
</ul>
```

## Abstände

### 100px Abstand (zwischen H2-Hauptabschnitten)
```html
<div style="height:100px" aria-hidden="true"></div>
```

### 50px Abstand (zwischen H3-Unterabschnitten)
```html
<div style="height:50px" aria-hidden="true"></div>
```

### 30px Abstand (vor/nach Hervorhebungen)
```html
<div style="height:30px" aria-hidden="true"></div>
```

## FAQ-Accordion

### HTML-Struktur
```html
<div class="faq-accordion">
  <details>
    <summary><strong>Erste Frage hier?</strong></summary>
    <p>Antwort auf erste Frage...</p>
  </details>
  <details>
    <summary><strong>Zweite Frage hier?</strong></summary>
    <p>Antwort auf zweite Frage...</p>
  </details>
  <details>
    <summary><strong>Dritte Frage hier?</strong></summary>
    <p>Antwort auf dritte Frage...</p>
  </details>
</div>
```

### Erforderliches CSS (im WordPress Theme)
```css
.faq-accordion details {
  background: #f8f9fa;
  border: 1px solid #e9ecef;
  border-radius: 8px;
  margin-bottom: 10px;
  padding: 0;
}
.faq-accordion summary {
  background: #f8f9fa;
  padding: 15px 20px;
  cursor: pointer;
  border-radius: 8px;
  font-weight: 600;
  color: #333;
  border-left: 4px solid #DD4067;
}
.faq-accordion summary:hover {
  background: #e9ecef;
}
.faq-accordion details[open] summary {
  border-bottom: 1px solid #e9ecef;
  border-radius: 8px 8px 0 0;
}
.faq-accordion details p {
  padding: 15px 20px;
  margin: 0;
  background: white;
  border-radius: 0 0 8px 8px;
}
```

## Code-Highlighting für User-Anpassungen

### HTML
```html
<span class="highlight-user">HIER_ANPASSEN</span>
```

### CSS
```css
.highlight-user {
  background-color: #DD4067;
  color: white;
  padding: 2px 4px;
  border-radius: 3px;
}
```

## Komplettes Artikel-Template

```html
<h1>Titel: Keyword + Nutzen (55-60 Zeichen)</h1>

<p>Conversational Einstieg: "Du suchst nach..." (100-150 Wörter)</p>

<div style="background-color: #f8f9fa; padding: 20px; border-left: 4px solid #DD4067; border-radius: 8px; margin: 20px 0;">
<p><strong>Kurz zusammengefasst:</strong></p>
<ul>
<li>Kernpunkt 1</li>
<li>Kernpunkt 2</li>
<li>Kernpunkt 3</li>
</ul>
</div>

<div style="height:100px" aria-hidden="true"></div>

<h2>Hauptabschnitt 1</h2>
<p>Content (200-300 Wörter, max 3-4 Sätze pro Absatz)...</p>

<div style="height:50px" aria-hidden="true"></div>

<h3>Unterabschnitt 1.1</h3>
<p>Details...</p>

<ul>
<li><strong>Punkt 1:</strong> Erklärung</li>
<li><strong>Punkt 2:</strong> Details</li>
</ul>

<div style="height:30px" aria-hidden="true"></div>

<div style="background-color: #f8f9fa; padding: 20px; border-left: 4px solid #DD4067; border-radius: 8px; margin: 20px 0;">
<p><strong>Wichtiger Hinweis:</strong> Zusätzliche Info...</p>
</div>

<div style="height:100px" aria-hidden="true"></div>

<h2>Hauptabschnitt 2</h2>
<p>Content...</p>

<!-- Weitere H2/H3 Sections... -->

<div style="height:100px" aria-hidden="true"></div>

<h2>Häufige Fragen (FAQ)</h2>

<div class="faq-accordion">
  <details>
    <summary><strong>Frage 1?</strong></summary>
    <p>Antwort 1...</p>
  </details>
  <details>
    <summary><strong>Frage 2?</strong></summary>
    <p>Antwort 2...</p>
  </details>
  <details>
    <summary><strong>Frage 3?</strong></summary>
    <p>Antwort 3...</p>
  </details>
</div>

<div style="height:100px" aria-hidden="true"></div>

<h2>Fazit</h2>
<p>Zusammenfassung + Call-to-Action...</p>
```

## Häufige Fehler (VERMEIDEN!)

### ❌ Falsche Formatierung
- Markdown-Syntax: `### Überschrift`, `**Bold**`
- Falscher Farb-Code: `#007cba` statt `#DD4067`
- Fehlende border-radius: Info-Boxen MÜSSEN `border-radius: 8px` haben
- Falsche Abstände: Nicht 50px zwischen H2 verwenden!

### ❌ Content-Fehler
- Artikel über 2.000 Wörter
- Sie-Form oder Wir-Form (exklusiv)
- Große Textblöcke ohne Absätze
- Keine Listen wo sinnvoll
- Fehlende "Kurz zusammengefasst" Box

### ❌ Tonalitäts-Fehler
- "Als ich Studien gelesen habe..."
- "Wissenschaftliche Belege zeigen..."
- Erfundene Tests/Erfahrungen
- Akademischer, roboterhafter Stil
