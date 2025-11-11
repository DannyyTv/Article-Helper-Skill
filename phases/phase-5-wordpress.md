# Phase 5: WordPress Upload

## Zweck

Diese Phase ladet den finalen, validierten HTML-Artikel zu WordPress als Draft hoch. Zusätzlich werden **Metadaten generiert** (H1 Titel + Meta-Description), die für SEO und WordPress-Publishing essentiell sind.

**OUTPUT:** `/Articles/[keyword-slug]/published/published.md`

---

## Tools in Phase 5

**Die KI nutzt FOLGENDE Tools in dieser Phase:**

| Schritt | Tool | Funktion |
|---------|------|----------|
| 1 | Read (lokal) | Phase 4 Validation-Daten + HTML laden |
| 2 | Claude (intern) | Metadaten generieren (Titel, Meta-Description) |
| 3 | `mcp__wordpress__create_wordpress_post` | Artikel als Draft hochladen |
| 4 | Write (lokal) | Phase 5 Info speichern |

**Obligatorisch:** Lokale Read/Write, WordPress MCP (Upload)

---

## ⚡ WICHTIG: Was die KI konkret tun muss

**NICHT NUR:** "Artikel ist fertig, hochladen?" sagen
**SONDERN:** Die Tools TATSÄCHLICH VERWENDEN um:
1. Phase 4 Validation-Daten lokal laden (`/Articles/[keyword-slug]/validation/validation.md`)
2. HTML aus `## 🔧 HTML-REFERENZ` extrahieren
3. Metadaten generieren (H1 Titel + Meta-Description)
4. User Metadaten zur Bestätigung zeigen
5. Via `mcp__wordpress__create_wordpress_post()` zu WordPress hochladen
6. WordPress Draft URL + Post ID speichern & anzeigen
7. Via Write (lokal) in `/Articles/[keyword-slug]/published/published.md` speichern

**Wenn eine Phase 5 Session beendet wird:**
- Der Artikel MUSS in WordPress als Draft vorhanden sein
- Phase 5 Daten (WordPress URL, Post ID) MÜSSEN lokal in `published.md` gespeichert sein
- Alles ist persistent!

---

## Workflow

### Schritt 1: Phase 4 HTML + Projekt-Daten laden

**Tool:** Lokale Read

**Die KI MUSS FOLGENDES TUN:**

1. Frage User nach `keyword-slug` (oder verwende aktive Session)

2. **Lade lokale Validation-Datei:**
   - Lese `/Articles/[keyword-slug]/validation/validation.md`
   - Extrahiere Markdown + `## 🔧 HTML-REFERENZ` Sektion
   - Extrahiere HTML aus der Referenz-Sektion
   - Speichere `keyword`, `html_content`

3. **Falls lokale Datei nicht verfügbar:**
   - Fehler anzeigen: "❌ Validation-Datei nicht gefunden"
   - User muss Phase 4 erneut durchlaufen

---

### Schritt 2: Metadaten generieren

#### 2.1 H1 Titel extrahieren & optimieren

**Die KI MUSS FOLGENDES TUN:**

1. Extrahiere `<h1>` aus HTML:
```regex
<h1>(.*?)</h1>
```

2. Prüfe Titel:
   - Länge: 55-60 Zeichen?
   - Format: "Keyword: Nutzen" oder "Keyword [Jahr]"?
   - Keyword vorhanden?

3. Falls zu kurz/lang: **Optimiere**
   - Zu lang: Kürzen, unwichtige Worte entfernen
   - Zu kurz: Nutzen/Vorteil hinzufügen
   - Aber: **Nicht verändern** wenn bereits optimal!

4. **Output:** Finaler WordPress Post Title
   ```
   Beispiel: "Pomodoro Technik: So strukturierst du deine Arbeitszeit" (57 Zeichen)
   ```

---

#### 2.2 Meta-Description generieren

**Die KI MUSS FOLGENDES TUN:**

1. **Quelle:**
   - H1 Titel (für Keyword)
   - Phase 4 Einleitung (`<p>` nach H1) - für Inhalt/Tonalität
   - Phase 1 Keyword - für SEO-Fokus

2. **Anforderungen:**
   - Länge: 155-160 Zeichen (SEO-optimal für Google)
   - Keyword: Am Anfang oder früh im Text
   - Hook: Nutzen/Vorteil deutlich machen
   - CTA oder Neugier: "Jetzt erfahren", "Entdecke", "Lerne"
   - Du-Form: Conversational bleiben
   - KEINE HTML-Tags oder Markdown

3. **Struktur:**
   ```
   [Keyword]: [Nutzen/Vorher-Nachher]. [Warum wichtig?]. [CTA/Hook].
   ```

4. **Beispiele:**

   ```
   ✅ "Pomodoro Technik: Strukturiere deine Arbeitszeit effektiv & steigere deine Produktivität. Lerne die beste Methode für tiefe Konzentration."
   (155 Zeichen)

   ✅ "Zeitmanagement für Anfänger: Praktische Tipps für mehr Kontrolle über deine Zeit. Entdecke erprobte Strategien für weniger Stress."
   (158 Zeichen)

   ❌ "POMODORO TECHNIK - ALLES WAS DU WISSEN MUSST!!!" (zu reißerisch, keine Längeninfo)
   ❌ "Die Pomodoro Technik ist eine <strong>Methode</strong> um..." (HTML-Tag, zu formal)
   ```

5. **Generiere & zeige dem User:**
   ```
   Meta-Description (155-160 Zeichen):
   "[Description]" ([X] Zeichen)

   Passt so? (OK / Feedback: [änderung])
   ```

6. **User-Feedback:**
   - "OK" → Weitermachen zu Schritt 3
   - "Feedback: ..." → Überarbeite Description, zurück zu 2.2

---

### Schritt 3: Metadaten-Bestätigung zeigen

**Die KI MUSS FOLGENDES TUN:**

1. Zeige User finale Metadaten:

```
📝 METADATEN FÜR WORDPRESS:

**Post Title:**
"[H1 Titel]" ([X] Zeichen, OK wenn 55-60)

**Meta-Description (SEO):**
"[Description]" ([X] Zeichen, OK wenn 155-160)

**Status:** Draft (User kann später publishen)

---

Sollen wir den Artikel zu WordPress hochladen? (J/N)
```

2. **User genehmigt oder lehnt ab:**
   - "J" / "OK" / "Los" → Weiter zu Schritt 4
   - "N" / "Nein" / "Feedback: ..." → Zurück zu Schritt 2 (überarbeiten)

---

### Schritt 3.5: FAQ Schema Generierung

**Die KI MUSS FOLGENDES TUN:**

Wenn der Artikel eine FAQ-Sektion hat (H2 "Häufige Fragen (FAQ)" mit `<details><summary>` Struktur):

**1. FAQ Schema erstellen:**

```json
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "@id": "[DOMAIN]/[ARTICLE-SLUG]/#faq-1",
      "name": "[FRAGE AUS SUMMARY]",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "[ANTWORT AUS P-ELEMENT]"
      }
    },
    {
      "@type": "Question",
      "@id": "[DOMAIN]/[ARTICLE-SLUG]/#faq-2",
      "name": "[NÄCHSTE FRAGE]",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "[ANTWORT]"
      }
    }
  ]
}
```

**Regeln:**
- `[DOMAIN]`: z.B. `https://mindsnapz.de`
- `[ARTICLE-SLUG]`: z.B. `pomodoro-technik-kritik`
- `@id`: Format `[DOMAIN]/[ARTICLE-SLUG]/#faq-[NUMBER]` (1, 2, 3...)
- `name`: Frage aus `<summary>` Text (ohne HTML)
- `text`: Antwort aus `<p>` Element(en) kombiniert (ohne HTML)

**2. In HTML einbinden:**
```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [...]
}
</script>
```

Position: Nach dem letzten `</p>` des Fazits, VOR WordPress Upload

**3. In `/Articles/[keyword-slug]/validation/validation.md` speichern** (zusammen mit HTML)

---

### Schritt 4: Zu WordPress hochladen via MCP

**Tool:** `mcp__wordpress__create_wordpress_post`

**Die KI MUSS FOLGENDES TUN:**

1. Rufe WordPress MCP auf:

```javascript
mcp__wordpress__create_wordpress_post({
  title: "[Finaler H1 Titel]",
  content: "[Komplettes finales HTML]",
  excerpt: "[Generierte Meta-Description]",
  status: "draft",
  categories: [],
  tags: []
})
```

**Parameter:**
- `title`: H1 Titel (55-60 Zeichen)
- `content`: Komplettes HTML aus Phase 4 (alle Sections, Styling, Abstände)
- `excerpt`: Meta-Description (155-160 Zeichen)
- `status`: IMMER "draft" (User entscheidet später über Publish!)
- `categories`: Leeres Array (User setzt später im WordPress Editor)
- `tags`: Leeres Array (User setzt später im WordPress Editor)

2. **Erfolgreiche Response:**
   - `post_id`: WordPress Post ID (z.B. `123`)
   - `link`: WordPress Draft URL (z.B. `https://websnapz.de/wp-admin/post.php?post=123&action=edit`)
   - `title`: Bestätigung des Titels
   - `date`: Publish-Datum (auto-gesetzt)

3. **Speichere folgende Daten:**
   - WordPress Post ID
   - Draft URL
   - Erfolgs-Timestamp

---

### Schritt 5: Erfolgs-Handling

#### 5.1 Upload erfolgreich ✅

**Die KI MUSS FOLGENDES TUN:**

1. Speichere WordPress-Daten:
   ```
   - post_id: [ID]
   - draft_url: [URL]
   - upload_timestamp: [Jetzt]
   ```

2. Zeige Erfolgs-Meldung:

```
✅ ARTIKEL ERFOLGREICH HOCHGELADEN!

**WordPress Draft:**
📝 Titel: "[H1 Titel]"
🔗 URL: [Draft Edit Link - als klickbar darstellen]
🆔 Post ID: [ID]

**Nächste Schritte:**
1. Öffne den Draft Link oben
2. Füge ein Featured Image hinzu (Bild/Thumbnail)
3. Final Review: Struktur, Formatierung, Links prüfen
4. Kategorien/Tags setzen (optional)
5. Publish wenn bereit!

**Tipp:** Der Artikel ist bereits vollständig formatiert - du kannst direkt publishen oder noch Änderungen im Editor vornehmen.
```

---

#### 5.2 Upload fehlgeschlagen ❌

**Die KI MUSS FOLGENDES TUN:**

1. **Fehler anzeigen:**
   ```
   ❌ UPLOAD FEHLGESCHLAGEN!

   Fehler: [Fehlermeldung vom WordPress MCP]
   ```

2. **Fehler-Debugging:**
   - HTML-Syntax prüfen? (Unclosed Tags, Special Characters?)
   - WordPress verbunden? (MCP aktiv?)
   - Berechtigungen? (Admin-Account aktiv?)

3. **Fallback Optionen:**
   ```
   Optionen:
   1. Erneut versuchen (J/N)?
   2. HTML als lokale Datei speichern + manuell hochladen?
   3. Fehler an Support melden?
   ```

4. **Falls Retry erfolgreich:** → Weitermachen zu Schritt 6

---

### Schritt 6: Phase 5 lokal speichern

**Tool:** Lokale Write

**Die KI MUSS FOLGENDES TUN:**

1. Schreibe WordPress-Daten lokal zu `/Articles/[keyword-slug]/published/published.md`:

```markdown
# Published: [KEYWORD]

## 🔗 Metadaten
- Keyword: [keyword]
- Title: [Artikel-Titel]
- Status: published
- Published Date: [Jetzt]

## 📝 WordPress Upload Info
- Post ID: [WordPress Post ID]
- Draft URL: [URL zum WordPress Draft]
- Upload Timestamp: [Timestamp]
- Meta-Description: "[Description]"

## 🔗 Original Content
[Link zu /Articles/[keyword-slug]/content/content.md]

## 🔧 Validation Reference
[Link zu /Articles/[keyword-slug]/validation/validation.md]
```

2. Speichere Phase 5 Daten persistent

---

### Schritt 7: Abschluss & Final Summary

**Die KI MUSS FOLGENDES TUN:**

1. Zeige Final Summary:

```
🎉 PROJEKT ABGESCHLOSSEN!

**Alle 5 Phasen erfolgreich:**
✅ Phase 1: Research & Competitor-Analyse → /Articles/[keyword-slug]/research/research.md
✅ Phase 2: Outline-Erstellung → /Articles/[keyword-slug]/outline/outline.md
✅ Phase 3: Content-Erstellung → /Articles/[keyword-slug]/content/content.md
✅ Phase 4: Validierung & HTML-Formatierung → /Articles/[keyword-slug]/validation/validation.md
✅ Phase 5: WordPress Upload → /Articles/[keyword-slug]/published/published.md

**Projekt-Status:** Completed
**Artikel:** [Titel]
**WordPress URL:** [Draft Link]

---

**Was jetzt?**
- Öffne den Draft Link oben
- Überprüfe Artikel im WordPress Editor
- Setze Featured Image + Kategorien/Tags
- Publish wenn bereit!

**Weitere Artikel erstellen?** (J/N)
```

---

## User-Kommunikation

- **Start:** "Lade Phase 4 HTML + Project-Daten... [Project: UUID]"
- **H1 Titel:** "Extrahierter Titel: '[Title]' ([X] Zeichen)"
- **Meta-Description:** "Generierte Meta-Description: '[Description]' ([X] Zeichen). Passt so?"
- **Metadaten-Check:** "Metadaten OK? Hochladen?"
- **Upload:** "Lade zu WordPress hoch..."
- **Erfolg:** "✅ Artikel hochgeladen! 🎉"
- **URL:** "Draft URL: [Link]" (als clickable Link)
- **Nächste Schritte:** "Öffne Draft → Featured Image → Publish"

---

## Error Handling

| Problem | Lösung |
|---------|--------|
| WordPress MCP nicht verfügbar | Fehler anzeigen, Fallback: HTML lokal speichern |
| HTML-Syntaxfehler im Upload | Phase 4 HTML prüfen, Unclosed Tags finden & fixen |
| Berechtigungen/Auth-Fehler | WordPress Credentials validieren, API-Key prüfen |
| Zu lange Meta-Description | Kürzen auf 160 Zeichen, Keywords behalten |
| Zu kurzer H1 Titel | Nutzen/Vorteil hinzufügen (max 60 Zeichen) |
| Supabase Fehler | Projekt UUID prüfen, Connection testen |

---

## Wichtige Punkte

- **IMMER Draft:** Status muss "draft" sein, niemals "publish" automatisch!
- **Metadaten zuerst:** H1 + Meta-Description VOR Upload generieren & bestätigen
- **WordPress MCP:** `mcp__wordpress__create_wordpress_post()` ist das zentrale Tool
- **Beide Storages:** Phase 5 Info in Supabase UND WordPress Draft als Source of Truth
- **User-Kontrolle:** User entscheidet über Publish, Featured Image, Kategorien
- **Final Status:** Projekt-Status MUSS auf "completed" sein am Ende
- **URL prominent:** Draft Link sollte klickbar & deutlich sichtbar sein

---

**Letzte Aktualisierung:** 2025-10-31
**Version:** 1.0 (Initial)
