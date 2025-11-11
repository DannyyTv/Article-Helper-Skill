# Phase 2: Outline-Erstellung

## Zweck

Diese Phase erstellt ein detailliertes Artikel-Outline basierend auf Phase 1 Erkenntnissen. Optional können externe Referenzen für spezifische Sektionen recherchiert werden. Das Outline definiert die exakte Struktur (H2/H3), Content-Punkte und Quellen für Phase 3.

**OUTPUT:** `/Articles/[keyword-slug]/outline/outline.md`

---

## Tools in Phase 2

**Die KI nutzt FOLGENDE Tools in dieser Phase:**

| Schritt | Tool | Funktion | Optional |
|---------|------|----------|----------|
| 1 | Read (lokal) | Phase 1 Daten laden aus `/Articles/[keyword-slug]/research/research.md` | Nein |
| 2.5 | Claude (intern) | Phase 1 Gaps parsen | Nein |
| 3 (Optional) | WebFetch | Content-Analyse für spezifische H2s | Ja |
| 4.5 | Write (lokal) | Outline `.md` Datei erstellen | Nein |

**Obligatorisch:** Lokale Read/Write
**Optional:** WebFetch (nur wenn User Research für spezifische H2s anfordert)

---

## ⚡ WICHTIG: Konkrete KI-Aktionen

1. Phase 1 Daten lokal laden: `/Articles/[keyword-slug]/research/research.md`
2. Gaps & Opportunities analysieren + WebFetch-Research empfehlen
3. Optional: WebFetch für User-definierte URLs durchführen
4. Finales Outline schreiben
5. Lokale Outline `.md` Datei in `/Articles/[keyword-slug]/outline/outline.md` erstellen (mit Metadaten, Opportunities, Interne Links, Outline, Quellen)
6. **Ergebnis MUSS persistent lokal sein vor Session-Ende**

---

## Workflow

### Schritt 1: Phase 1 Daten laden

**Tool:** Lokale Read

**Die KI MUSS FOLGENDES TUN:**

1. Frage User nach `keyword-slug` (oder verwende aktive Session)

2. **Lade Phase 1 Daten lokal:**
   - Lese `/Articles/[keyword-slug]/research/research.md`
   - Extrahiere Opportunities, Content Gaps, Key Findings, Interne Links

3. Parse die Phase 1 Daten:
   - Opportunities identifizieren
   - Content Gaps auslesen
   - Key Findings verstehen
   - Interne Links extrahieren

---

### Schritt 2: Grobe Struktur zeigen

Basierend auf Phase 1 Opportunities + Key Findings dem User die geplante H2-Struktur zeigen. Ergänze mit FAQ am Ende.

---

### Schritt 2.5: Gaps & Opportunities analysieren

Extrahiere aus Phase 1:
- TOP 3 Opportunities
- Content Gaps (was Competitors nicht machen)

Empfehle dem User WebFetch-Research für H2s wo die größten Gaps liegen. User entscheidet für welche H2s recherchiert werden soll.

---

### Schritt 3: Research durchführen (OPTIONAL via WebFetch)

Nur für vom User ausgewählte H2s:

1. User gibt 2-3 URLs pro H2 an
2. WebFetch nutzen um zu extrahieren: Hauptpunkte, Tools/Ressourcen, Statistiken, Zitate, relevante Sektionen
3. Findings in Outline integrieren mit Quellenangaben

---

### Schritt 4.: Lokale `.md` Datei erstellen

**Tool:** Write (lokal)

Erstelle eine neue Datei: `/Articles/[keyword-slug]/outline/outline.md`

Diese Datei enthält alle Infos für Phase 3 (Metadaten, Opportunities, Interne Links, Outline, Quellen):

```markdown

## 🔗 Metadaten
- Keyword: [keyword]
- Title: [Artikel-Titel]

## 📚 Phase 1 Opportunities
- [Opportunity 1 - konkret]
- [Opportunity 2 - konkret]
- [Opportunity 3 - konkret]

## 🔗 Interne Links (gefunden in Phase 1)
- [Anchor Text](WordPress Post ID)
- [Anchor Text](WordPress Post ID)

Alle H2s kombinieren mit dieser Struktur:

# Outline: [KEYWORD]

## H2: [Titel]
### H3: Unterpunkt
- Content Punkt
- Content Punkt
[Weitere H3s...]

**Recherchierte Quellen (falls vorhanden):**
- [Quelle](URL)

## [Weitere H2s...]

## FAQ
- Longtail-Frage 1?
- Longtail-Frage 2?
```

**Guidelines:**
- H2 → H3 → Content-Punkte (flexible Anzahl)
- Quellen wenn vorhanden
- FAQ am Ende mit Longtail-Fragen
```markdown

---

**Nach Datei-Erstellung:** "✅ `.md` erstellt unter `/Articles/[keyword-slug]/outline/outline.md`"

---

### Schritt 5: Abschluss Phase 2

**Nach Datei-Speicherung:**
- "✅ Phase 2 abgeschlossen!"
- Lokale `.md` ist in `/Articles/[keyword-slug]/outline/outline.md`
- "Bereit für Phase 3?"
