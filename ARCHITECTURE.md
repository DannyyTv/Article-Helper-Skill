# Websnapz Article Writer - Finale Architektur

## Übersicht

Die Websnapz Article Writer ist ein spezialisierter Claude Skill für strukturierte SEO-Artikel-Erstellung mit folgendem Aufbau:

```
Skill (SKILL.md)
├── Phases (5-Phase Workflow)
│   ├── Phase 1: Research & Competitor-Analyse (phase-1-research.md)
│   ├── Phase 2: Outline-Erstellung (phase-2-outline.md)
│   ├── Phase 3: Content-Erstellung (phase-3-content.md)
│   ├── Phase 4: Validierung & HTML-Formatierung (phase-4-validation.md)
│   └── Phase 5: WordPress Upload (phase-5-wordpress.md)
├── Persistierung (Lokale Keyword-basierte Ordner)
│   └── /Articles/[keyword-slug]/
│       ├── research/research.md (Phase 1)
│       ├── outline/outline.md (Phase 2)
│       ├── content/content.md (Phase 3)
│       ├── validation/validation.md (Phase 4)
│       └── published/published.md (Phase 5)
├── Integration (MCP Tools)
│   ├── WordPress (Content Management)
│   └── WebFetch (Research & Content Analysis)
└── Formatting & Guidelines
    ├── formatting-guide.md
    └── SKILL.md (Tonalität & HTML Rules)
```

---

## Persistierungs-Architektur (Lokal)

### Ordnerstruktur

Alle Artikel werden in **Keyword-basierten Ordnern** persistiert:

```
/Articles/
├── pomodoro-technik/
│   ├── research/
│   │   └── research.md (Phase 1 Ergebnisse)
│   ├── outline/
│   │   └── outline.md (Phase 2 Ergebnisse)
│   ├── content/
│   │   └── content.md (Phase 3 Content - Markdown)
│   ├── validation/
│   │   └── validation.md (Phase 4 Content - Markdown + HTML)
│   └── published/
│       └── published.md (Phase 5 WordPress Info)
│
├── agile-methodik/
│   └── [Gleiche Struktur]
```

### Datei-Format

Jede Phase-Datei ist **Markdown-basiert** mit folgender Struktur:

**research.md:**
```markdown
# Research: [KEYWORD]

## 🔗 Metadaten
- Keyword: [keyword]
- Title: [Artikel-Titel]
- Keyword-Slug: [slug]
- Status: in_progress

## 🏆 Top 3 Opportunities
...

## 🌐 Competitor-Analyse
...
```

**outline.md, content.md, validation.md, published.md:**
Ähnliche Struktur mit phasenspezifischen Metadaten und Inhalten.

**validation.md** hat zusätzlich eine HTML-Referenz-Sektion:
```markdown
## 🔧 HTML-REFERENZ

[Komplettes HTML mit allen Formatierungen]
```

### Keine Datenbank-Abhängigkeit

- ✅ Alle Daten sind **lokal persistent** in Markdown-Dateien
- ✅ **Keine Supabase-Abhängigkeit** für Phase-Speicherung
- ✅ **Einfaches Backup:** Einfach `/Articles/` Ordner sichern
- ✅ **Verbesserter Kontext:** Keine großen DB-Queries nötig

---

## 5-Phasen Workflow

### Phase 1: Research & Competitor-Analyse
**Input:** Keyword
**Tools:** WebFetch (Content Analysis), WordPress MCP (Internal Search)
**Output:** Research-Markdown mit Competitor-Analyse, Content Gaps, Opportunities
**Speicherung:** Lokal in `/Articles/[keyword-slug]/research/research.md`

**Key Activities:**
- Web Search: Top 5 Competitor-Artikel finden
- Content Crawling: Struktur, Tonalität, Formate analysieren
- Weakness Analysis: TOP 3 Artikel auf 8 Schwäche-Kategorien prüfen
- Opportunities: Identifizieren was WIR besser machen können
- WordPress Search: Ähnliche eigene Artikel suchen

### Phase 2: Outline-Erstellung
**Input:** Phase 1 Research & Opportunities (lokal geladen)
**Tools:** Claude (Analysis & Writing), WebFetch (Optional Research)
**Output:** Detailliertes Artikel-Outline mit H2/H3 Struktur
**Speicherung:** Lokal in `/Articles/[keyword-slug]/outline/outline.md`

### Phase 3: Content-Erstellung
**Input:** Phase 2 Outline + Phase 1 Research (lokal geladen)
**Tools:** Claude (Content Writing), WebFetch (Quellen-Recherche)
**Output:** Finaler Artikel-Content (Markdown, keine Formatierung)
**Speicherung:** Lokal in `/Articles/[keyword-slug]/content/content.md`

### Phase 4: Validierung & HTML-Formatierung
**Input:** Phase 3 Content (lokal geladen)
**Tools:** Claude (QA & Analysis, HTML Konvertierung)
**Output:** Validierter Content + HTML mit Formatierung
**Speicherung:** Lokal in `/Articles/[keyword-slug]/validation/validation.md`

### Phase 5: WordPress Upload
**Input:** Phase 4 Validation (lokal geladen, HTML extrahiert)
**Tools:** WordPress MCP (`create_wordpress_post`), Claude (Metadaten-Generierung)
**Output:** WordPress Draft URL, Post ID, Upload-Info
**Speicherung:** Lokal in `/Articles/[keyword-slug]/published/published.md`

---

## MCP Integration

### WebFetch & Web Research
- `WebFetch` - Content-Analyse von Competitor-URLs
- `web_search` - Keyword-Recherche
- Für Phase 1-3: Content Extraction & Analysis

### WordPress MCP
- `list_wordpress_posts` - Ähnliche Artikel suchen
- `get_wordpress_post` - Artikel-Details laden
- `create_wordpress_post` - Artikel zu WordPress hochladen (Phase 5)

### Keine Supabase-Abhängigkeit mehr
- ✅ Alle Persistierung erfolgt **lokal** via Read/Write
- ✅ Keine SQL Queries mehr nötig
- ✅ Reduzierter Kontext-Overhead

---

## Setup Instructions

### 1. Lokale Ordnerstruktur vorbereiten
```bash
mkdir -p /Users/[user]/.claude/skills/websnapz-article-writer/Articles
```

### 2. MCP Configuration
In `~/.claude/claude-desktop-config.json`:
```json
{
  "mcpServers": {
    "wordpress": { ... }
  }
}
```

### 3. Environment Variables (nur WordPress)
- `WORDPRESS_URL` - WordPress Site URL
- `WORDPRESS_USERNAME` - WordPress User
- `WORDPRESS_PASSWORD` - WordPress App Password

### 4. Keine Supabase-Konfiguration mehr nötig ✅
- Supabase-Abhängigkeit vollständig entfernt
- Alle Daten werden lokal persistiert

---

## Datei-Struktur

| Datei | Zweck |
|-------|-------|
| `SKILL.md` | Skill Entry Point, Formatierungs-Rules, Tonalität |
| `phases/phase-1-research.md` | Phase 1 Detaillierte Anweisungen |
| `phases/phase-2-outline.md` | Phase 2 Detaillierte Anweisungen |
| `phases/phase-3-content.md` | Phase 3 Detaillierte Anweisungen |
| `phases/phase-4-validation.md` | Phase 4 Detaillierte Anweisungen |
| `phases/phase-5-wordpress.md` | Phase 5 Detaillierte Anweisungen |
| `supabase-schema.sql` | Datenbank-Schema (SQL) |
| `supabase-queries.md` | SQL Query Referenz & Beispiele |
| `wordpress-integration.md` | WordPress MCP Tool Dokumentation |
| `formatting-guide.md` | HTML/Formatierungs-Standards |
| `ARCHITECTURE.md` | Diese Datei |

---

## Design Decisions

### Warum flache Phasen-Struktur (nicht normalisiert)?
- **Bessere Performance:** Ein Query für alle Phasen
- **Klarerer Kontext:** Jede Phase hat eigene Spalten
- **Einfacherer Code:** Keine JOIN-Operationen nötig
- **Saubere Abgrenzung:** Jede Phase ist klar separiert

### Warum keine pgvector (Embeddings)?
- **Overengineering:** Nicht nötig für aktuelle Use-Cases
- **Kostenersparnisse:** Keine zusätzlichen Gebühren
- **Komplexität:** Vereinfachte Wartbarkeit

### Warum Supabase statt andere DB?
- **MCP Support:** Native Integration mit Claude
- **PostgreSQL:** Bewährte, robuste Datenbank
- **Skalierung:** Automatische Backups, Replicas
- **API-First:** RESTful & Realtime APIs included

---

## Fehlerbehandlung

### Common Issues

| Problem | Lösung |
|---------|--------|
| Exa API Rate Limit | Wartezeit einbauen oder allgemeinere Keywords nutzen |
| Content Crawling schlägt fehl | Fallback auf Snippet + Metadaten |
| WordPress Post nicht erstellbar | Formatierungs-Fehler in HTML prüfen |
| Supabase Connection Fehler | API Key & URL validieren |

---

## Design Decisions (v2.0 - Optimiert)

### Warum lokale Persistierung?
- **Effizienz:** Keine Netzwerk-Latenz für Phase-Speicherung
- **Kontext-Einsparung:** Weniger Token für DB-Queries
- **Einfachheit:** Markdown ist lesbar und versionierbar
- **Portabilität:** Einfaches Backup (nur `/Articles/` Ordner)
- **Offline-Fähigkeit:** Funktioniert auch ohne Internetverbindung

### Warum Keyword-Slug statt UUID?
- **Benutzerfreundlich:** Ordnernamen sind aussagekräftig
- **Navigierbar:** Einfaches Auffinden ohne Datenbank-Lookup
- **SEO-fokussiert:** Keyword ist zentral für den Artikel

### Wann ist WordPress MCP noch nötig?
- **Nur in Phase 5:** Für finalen Upload zu WordPress
- **Keine Persistierung-Abhängigkeit:** Optional für Entwürfe

---

**Letzte Aktualisierung:** 2025-11-10
**Version:** 2.0 (Lokale Keyword-basierte Persistierung)
