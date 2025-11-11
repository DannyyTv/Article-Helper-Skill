# Phase 1: Research & Competitor-Analyse

## Zweck

Diese Phase recherchiert Competitor-Artikel und interne Artikel zum Keyword. Das Ziel ist, Erkenntnisse über Struktur, Tonalität, Formatting und interne Verlinkung zu sammeln. Diese Erkenntnisse werden die Grundlage für Phase 2-5.

**OUTPUT:** `/Articles/[keyword-slug]/research/research.md`

---

## Tools in Phase 1

**Die KI nutzt FOLGENDE Tools in dieser Phase:**

| Schritt | Tool | Funktion | Beschreibung |
|---------|------|----------|-------------|
| 1 | Bash/Write (lokal) | Ordner erstellen | Keyword-Slug Ordnerstruktur anlegen |
| 2 | WebFetch | Content-Analyse | Competitor-Artikel analysieren |
| 3 | `wordpress` | list_wordpress_posts | Eigene Artikel suchen |
| 3 | `wordpress` | get_wordpress_post | Artikel-Details laden |
| 5 | Write (lokal) | Research `.md` erstellen | Research-Daten lokal speichern |

---

## ⚡ WICHTIG

**NICHT NUR:** Markdown schreiben
**SONDERN:** Tools VERWENDEN (WebFetch analysiert, WordPress sucht, Write erstellt lokale `.md`)

Alle Daten MÜSSEN lokal in `/Articles/[keyword-slug]/research/research.md` gespeichert sein bevor Phase 1 endet!

---

## Verzeichnis-Struktur

```
/Articles/[keyword-slug]/
└── research/
    └── research.md (Research-Daten - wird in Schritt 1.5 erstellt)
```

**Beispiel:** `/Articles/pomodoro-technik/research/research.md`

---

## Workflow

### Schritt 1: Keyword-Input & File erstellen

1. Frage User: "Welches Keyword/Thema für den neuen Artikel?"
2. Generiere **Keyword-Slug** aus User-Input:
   - Beispiel: "Die Pomodoro Technik" → `pomodoro-technik`
   - Regel: Kleinbuchstaben, Bindestriche, keine Sonderzeichen
3. Erstelle Ordnerstruktur:
   ```
   /Articles/[keyword-slug]/
   ├── research/
   ```
4. Zeige User den Keyword-Slug zur Bestätigung:
   ```
   ✅ Ordnerstruktur erstellt: /Articles/[keyword-slug]/
   Keyword-Slug: [keyword-slug]
   Bereit für Research?
   ```

---

### Schritt 2: Competitor-Recherche via WebFetch

1. Frage User: "Top 5 Konkurrenz-Artikel? (URLs eingeben)"
2. Nutze WebFetch für jede URL und analysiere:

| Kriterium | Was prüfen |
|-----------|-----------|
| **Wortanzahl** | Gesamt Word Count |
| **Struktur** | Anzahl H2 + H3 |
| **Tonalität** | Conversational? Du-Form? |
| **Formate** | Info-Boxen, Listen, Tables, FAQ, Videos |
| **Absätze** | Durchschnittliche Länge |
| **Links** | Welche Artikel werden verlinkt |

3. Dokumentiere alle Findings + Besonderheiten pro Artikel

---

### Schritt 2.1: Quellen-Empfehlung für Phase 3

**Primär:** ResearchGate, Google Scholar, Fachjournale, Uni-Publikationen, Studien
**Sekundär:** Expertenartikel mit Quellen, Whitepapers, offizielle Quellen
**Nicht:** Blogs ohne Quellen, Social Media, Quellen >5 Jahre

---

### Schritt 2.5: Schwächen-Identifikation & Opportunities (Top 3 Artikel)

**Für die TOP 3 Competitor-Artikel prüfen:**

| Schwäche-Kategorie | Frage | Beispiel |
|-------------------|-------|----------|
| **Content Gaps** | Welche wichtigen Unterthemen fehlen? | "Keine Tipps zu digitalen Tools" |
| **Praktische Beispiele** | Sind nur Theorie oder konkrete, verwendbare Beispiele vorhanden? | "Nur generische Tipps, keine Step-by-Step Anleitung" |
| **Aktualität** | Sind Daten, Statistiken, Trends aktuell (2024/2025)? | "Zitiert 2019 Statistiken" |
| **Autorität/Quellen** | Werden Experten zitiert? Sind Quellen verlinkt? | "Keine Quellen angegeben" |
| **Tiefe vs. Breite** | Ist der Content zu oberflächlich oder zu technisch für Zielgruppe? | "Nur oberflächliche Erklärungen" |
| **Actionable Insights** | Kann der Reader konkret etwas damit anfangen? | "Tipps sind zu vage" |
| **Struktur/Navigation** | Ist schnell zu finden, was man sucht? Zu viele lange Blöcke? | "Große Absätze, schwer zu scannen" |
| **Vergleiche/Alternativen** | Werden Alternativen, Pro/Contra oder Vergleiche gezeigt? | "Nur eine Perspektive, keine Vergleiche" |

**Dokumentiere** konkrete Beispiele für identifizierte Schwächen

---

### Schritt 2.6: Opportunities für deinen Artikel

Basierend auf den identifizierten Schwächen, erstelle eine **Opportunities Liste**:

```markdown
## Opportunities - Was WIR besser machen können

### Content Gaps (Themen, die fehlen)
- **Gap 1:** [Thema/Unterpunkt] - in keinem Competitor erwähnt
  - Relevanz für Zielgruppe: HOCH/MITTEL
  - Geplant als: Neuer H2 Abschnitt

- **Gap 2:** [Anderes Thema] - nur oberflächlich erwähnt
  - Relevanz: HOCH
  - Geplant als: Ausführlicher H2 + H3 + Praktische Beispiele

### Praktische Verbesserungen
- **Bessere Beispiele:** Konkrete Step-by-Step Anleitung statt nur Theorie
- **Tools & Ressourcen:** Spezifische Apps, Templates, Checklisten empfehlen
- **Aktuelle Daten:** 2024/2025 Trends und Statistiken einfügen

### Struktur & Format Verbesserungen
- **Bessere Scanbarkeit:** Mehr Subheadings, kürzere Absätze
- **Vergleichs-Element:** Pro/Contra oder Alternativen-Tabelle
- **Info-Boxen:** Key Takeaways hervorheben
- **FAQ:** Häufige Fragen separat behandeln

### Unique Selling Points (Was nur WIR haben)
- **Punkt 1:** [Was die Competitors nicht machen]
- **Punkt 2:** [Unser Unique Angle]
- **Punkt 3:** [Besonderer Fokus/Perspektive]
```

---

### Schritt 3: WordPress Internal Search - Eigene Artikel finden
Nutze Wordpress MCP Tools
1. Nutze `list_wordpress_posts` um ähnliche Artikel zu finden:
   - Search: [Keyword] | per_page: 10 | orderby: relevance
2. Für relevante Matches: Hole Details via `get_wordpress_post`
3. Analysiere wie Competitors (Struktur, Tonalität, Länge, Formate)

---

### Schritt 4: Key Findings dokumentieren

Erstelle diese Insights aus der Analyse:
- **Struktur:** Durchschnittliche H2-Anzahl, H3 pro H2, Standard-Wortanzahl
- **Tonalität:** Conversational? Du-Form? Persönliche Erfahrungen?
- **Formate:** Info-Boxen, Listen, FAQ, Tables, Videos (welche häufig?)
- **Links:** Durchschnitt pro Artikel, meist verlinkte Topics

---

### Schritt 5: Lokale Research-Datei erstellen

**Tool:** Write (lokal)

Erstelle eine neue Datei: `/Articles/[keyword-slug]/research/research.md`

Diese Datei enthält alle Research-Daten für Phase 2 (Metadaten, Opportunities, Links, Competitor-Analyse, Schwächen, Insights):

```markdown
# Research: [KEYWORD]

## 🔗 Metadaten
- Keyword: [keyword]
- Title: [Artikel-Titel]
- Keyword-Slug: [keyword-slug]
- Status: in_progress
- Created: [Datum]

## 🏆 Top 3 Opportunities
- [Opportunity 1 - konkret]
- [Opportunity 2 - konkret]
- [Opportunity 3 - konkret]

## 🔗 Interne Links (gefunden in Phase 1)
- [Anchor Text](WordPress Post ID)
- [Anchor Text](WordPress Post ID)

## 🌐 Competitor-Analyse (Top 5)

### 1. [Titel](URL)
- Wörter: X
- Struktur: X H2, X H3
- Tonalität: [Du-Form?]
- Besonderheiten: [liste]

### 2. [Titel](URL)
[Gleiche Struktur]

## 🔍 Schwächen (Top 3 Artikel)

| Schwäche-Kategorie | Wo? | Beispiel |
|-------------------|-----|----------|
| Content Gaps | Artikel 1 | [konkrete Lücke] |
| Praktische Beispiele | Artikel 2 | [nur Theorie] |

## 💡 Eigene Artikel (gefunden)
- [Artikel Title](WordPress Link) - [Struktur, Tonalität]
- [Artikel Title](WordPress Link)

## 📊 Key Insights für Phase 2
- **Struktur:** [durchschnittliche H2-Anzahl, H3 pro H2]
- **Tonalität:** [conversational? Du-Form?]
- **Formate:** [Info-Boxen, FAQ, Lists - häufig genutzt]
- **Links:** [durchschnitt pro Artikel]
```

**Nach Datei-Erstellung:** "✅ Research gespeichert unter `/Articles/[keyword-slug]/research/research.md`"

---

### Schritt 6: Abschluss Phase 1

Nach Speicherung der lokalen `.md` Datei:

1. **Bestätige:** ✅ Phase 1 abgeschlossen
2. **Zeige:** TOP 3 Opportunities + Key Insights
3. **Bestätige Speicherung:**
   - Research `.md` erstellt unter `/Articles/[keyword-slug]/research/research.md`
4. **Frage:** "Bereit für Phase 2 (Outline)? (J/N)"

---

## MCP Tool-Referenzen

- **WebFetch:** Für Content-Analyse von URLs
- **WordPress MCP:** [wordpress-integration.md](../wordpress-integration.md)
- **Write (lokal):** Für Markdown-Datei-Speicherung
