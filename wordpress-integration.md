# WordPress MCP Integration Guide

Dieser Guide erklärt, wie der Article Writer Skill WordPress MCP Tools nutzt für Referenz-Artikel-Analyse und Upload.

## Verfügbare WordPress MCP Tools

### 1. `mcp__wordpress__list_wordpress_posts`
**Zweck:** Existierende Artikel suchen/filtern

**Parameter:**
```javascript
{
  search: "Keyword",           // Suchbegriff
  per_page: 10,                 // Anzahl Ergebnisse (1-100)
  status: "publish",            // "publish", "draft", "any"
  orderby: "date",              // "date", "relevance", "title"
  order: "desc",                // "asc" oder "desc"
  include_content: false        // Content-Preview inkludieren?
}
```

**Verwendung im Skill:**
```javascript
// Finde ähnliche Artikel zum Thema
const posts = await mcp__wordpress__list_wordpress_posts({
  search: user_keyword,
  per_page: 5,
  status: "publish",
  orderby: "relevance",
  include_content: false
});

// Identifiziere besten Match basierend auf Titel-Ähnlichkeit
const best_match = posts[0];
```

---

### 2. `mcp__wordpress__get_wordpress_post`
**Zweck:** Kompletten Artikel-Content abrufen

**Parameter:**
```javascript
{
  id: 123,                      // Post ID (required)
  context: "edit"               // "view", "embed", "edit"
}
```

**Verwendung im Skill:**
```javascript
// Hole vollständigen Referenz-Artikel
const reference_article = await mcp__wordpress__get_wordpress_post({
  id: best_match.id,
  context: "edit"
});

// Analysiere Struktur
const analysis = {
  h2_count: count_h2_tags(reference_article.content),
  h3_count: count_h3_tags(reference_article.content),
  word_count: count_words(reference_article.content),
  has_summary: reference_article.content.includes("Kurz zusammengefasst"),
  has_faq: reference_article.content.includes("faq-accordion"),
  info_box_count: count_info_boxes(reference_article.content),
  uses_du_form: check_du_form(reference_article.content)
};
```

---

### 3. `mcp__wordpress__create_wordpress_post`
**Zweck:** Neuen Artikel hochladen

**Parameter:**
```javascript
{
  title: "Artikel-Titel",      // Required, max 255 Zeichen
  content: "<html>...</html>", // Required, vollständiger HTML-Content
  status: "draft",             // "publish", "draft", "private"
  excerpt: "Meta-Description", // Optional, 155 Zeichen für SEO
  categories: [1, 5],          // Optional, Category IDs
  tags: [10, 12, 15]           // Optional, Tag IDs
}
```

**Verwendung im Skill:**
```javascript
// Upload fertigen Artikel als Draft
const new_post = await mcp__wordpress__create_wordpress_post({
  title: final_title,
  content: final_html_content,
  status: "draft",
  excerpt: meta_description
});

// Gib User die Post-URL
console.log(`Artikel als Draft erstellt: ${new_post.link}`);
```

---

### 4. `mcp__wordpress__get_wordpress_categories`
**Zweck:** Verfügbare Kategorien abrufen

**Parameter:**
```javascript
{
  per_page: 100,               // Max 100
  page: 1
}
```

**Verwendung im Skill:**
```javascript
// Zeige User verfügbare Kategorien zur Auswahl
const categories = await mcp__wordpress__get_wordpress_categories({
  per_page: 100
});

// Lasse User Kategorie wählen
console.log("Verfügbare Kategorien:");
categories.forEach(cat => console.log(`- ${cat.name} (ID: ${cat.id})`));
```

---

### 5. `mcp__wordpress__get_wordpress_tags`
**Zweck:** Verfügbare Tags abrufen

**Parameter:**
```javascript
{
  per_page: 100,
  page: 1
}
```

---

## Skill Workflow mit WordPress MCP

### Phase 1: Research & Referenz-Artikel finden

```
1. User gibt Thema/Keyword: "Zeitmanagement Apps"

2. Suche nach ähnlichen Artikeln:
   mcp__wordpress__list_wordpress_posts({
     search: "Zeitmanagement",
     per_page: 5,
     status: "publish",
     orderby: "relevance"
   })

3. Falls Ergebnisse > 0:
   - Zeige User die Top 3 Matches
   - Frage: "Welcher Artikel soll als Style-Referenz dienen?"
   - Oder: Automatisch besten Match wählen

4. Hole kompletten Referenz-Artikel:
   mcp__wordpress__get_wordpress_post({
     id: selected_post_id,
     context: "edit"
   })

5. Analysiere Referenz-Artikel:
   - Struktur: Anzahl H2/H3, "Kurz zusammengefasst" vorhanden?, FAQ vorhanden?
   - Tonalität: Du-Form konsistent?, conversational?
   - Formatierung: Info-Boxen mit #DD4067?, korrekte Abstände?
   - Länge: Wort-Count, durchschnittliche Section-Länge

6. Falls keine Referenz gefunden:
   - Warne User: "Kein ähnlicher Artikel gefunden, nutze Standard-Template"
   - Fahre mit Standard-Struktur fort
```

### Phase 2: Outline erstellen mit Referenz-Anpassung

```
1. Erstelle Outline basierend auf:
   - Standard-Template (3-4 H2 Sections)
   - Referenz-Artikel Struktur (falls vorhanden)
   - User-Keyword/Thema

2. Zeige Outline:
   "Geplante Struktur (angelehnt an Referenz-Artikel 'XY'):

   H1: [Titel-Vorschlag]
   - Einleitung (100-150 Wörter)
   - Kurz zusammengefasst Box

   H2: [Section 1 Titel]
     H3: [Subsection 1.1]
     H3: [Subsection 1.2]

   H2: [Section 2 Titel]
   ...

   H2: FAQ (3-5 Fragen)
   H2: Fazit + CTA

   Geschätzte Länge: ~1.800 Wörter"

3. Warte auf User-Approval: "OK?" oder "Anpassen?"
```

### Phase 3: Content-Erstellung mit Style-Transfer

```
1. Schreibe Artikel-Sections
2. Übernehme aus Referenz-Artikel:
   - Tonalität (conversational, Du-Form)
   - Struktur-Patterns (z.B. "Lass uns schauen...", "Du kennst sicher...")
   - Formatierungs-Stil (Info-Boxen-Platzierung, Listen-Häufigkeit)
3. Befolge STRIKT ArticleRules.md Limits (2.000 Wörter, etc.)
```

### Phase 4: Validierung

```
1. Prüfe gegen Checkliste (siehe instructions.md)
2. Zeige Ergebnisse:
   "✅ Titel: 58 Zeichen (OK)
   ✅ Meta-Description: 152 Zeichen (OK)
   ✅ Wort-Count: 1.847 Wörter (OK)
   ❌ Info-Box Zeile 45: Nutzt #007cba statt #DD4067
   ✅ Alle Abstände korrekt
   ✅ Du-Form durchgehend"
3. Biete Auto-Fix für Probleme
```

### Phase 5: WordPress Upload

```
1. Frage User: "Als Draft hochladen? (Ja/Nein)"

2. Falls Ja:
   a) Zeige verfügbare Kategorien:
      mcp__wordpress__get_wordpress_categories()

   b) Frage: "Kategorie wählen? (Optional, Enter für keine)"

   c) Upload:
      mcp__wordpress__create_wordpress_post({
        title: final_title,
        content: validated_html,
        status: "draft",
        excerpt: meta_description,
        categories: [user_selected_category_id]  // falls gewählt
      })

   d) Gib Erfolgs-Meldung:
      "✅ Artikel erfolgreich hochgeladen!
      📝 Draft-URL: https://websnapz.com/wp-admin/post.php?post=123&action=edit

      Nächste Schritte:
      - Review im WordPress Editor
      - Featured Image hinzufügen
      - Kategorie/Tags final setzen
      - Publish!"

3. Falls Nein:
   "Artikel als HTML-Datei speichern? (Optional)"
```

---

## Error Handling

### WordPress MCP nicht verfügbar
```
if (!mcp_available) {
  console.log("⚠️ WordPress MCP nicht verbunden.");
  console.log("Fahre ohne Referenz-Artikel fort (Standard-Template).");
  // Continue with standard workflow
}
```

### Keine Referenz-Artikel gefunden
```
if (search_results.length === 0) {
  console.log("ℹ️ Keine ähnlichen Artikel gefunden.");
  console.log("Nutze Standard Websnapz-Template.");
  // Use article-structure.html template
}
```

### Upload fehlgeschlagen
```
try {
  const post = await mcp__wordpress__create_wordpress_post({...});
} catch (error) {
  console.log("❌ Upload fehlgeschlagen:", error.message);
  console.log("Artikel als HTML-Datei speichern?");
  // Offer local file save as fallback
}
```

---

## Best Practices

### 1. Immer User-Approval für Outline
- Zeige vollständige geplante Struktur
- Warte auf explizites "OK" oder "Los"
- Erlaube Anpassungen vor Content-Erstellung

### 2. Transparenz bei Referenz-Artikel-Nutzung
- Zeige User welcher Artikel als Referenz dient
- Erkläre kurz: "Übernehme Struktur/Tonalität von Artikel XY"
- Lasse User alternative Referenz wählen falls gewünscht

### 3. Draft als Standard
- IMMER status: "draft" beim Upload
- Niemals direkt "publish" ohne explizite User-Anfrage
- Gib User finale Kontrolle im WordPress Editor

### 4. Validierung vor Upload
- Führe IMMER vollständige Checkliste durch
- Fixe kritische Fehler automatisch (Farben, Abstände)
- Zeige User alle Validierungs-Ergebnisse

### 5. URL nach Upload prominent anzeigen
- User muss sofort Draft im WP-Admin öffnen können
- Zeige auch nächste Schritte (Featured Image, etc.)
