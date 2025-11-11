# Article Helper Skill

Ein professioneller Claude Skill für vollautomatisierte Artikel-Erstellung mit SEO-Optimierung, WordPress-Integration und mehrstufiger Validierung.

## Features

- 🔍 **Research-Phase** - Automatische Recherche & Referenz-Artikel-Analyse
- 📋 **Outline-Generation** - Intelligente Struktur-Planung
- ✍️ **Content-Erstellung** - KI-gestützte Texterstellung mit Style-Transfer
- ✅ **Validierung** - Automatische SEO-, Format- & Qualitätsprüfung
- 📤 **WordPress-Upload** - Direkter Upload als Draft (optional)

## Voraussetzungen

- Node.js installiert
- Claude IDE / Claude Code mit Skill-Support
- WordPress-Website mit aktiviertem MCP-Server (optional, für Phase 5)

## Installation

### 1. Skill-Verzeichnis konfigurieren

```bash
# Kopiere diesen Ordner in dein `.claude/skills/` Verzeichnis
cp -r Article-Helper-Skill ~/.claude/skills/

# Oder nutze den Ordner direkt von hier
```

### 2. WordPress MCP Server Konfiguration (Optional)

Falls du WordPress-Integration nutzen möchtest:

**a) `.mcp.json` erstellen:**

```bash
cp .mcp.json.example .mcp.json
```

**b) `.mcp.json` mit deinen Daten befüllen:**

```json
{
  "mcpServers": {
    "wordpress": {
      "command": "node",
      "args": [
        "/path/to/your/wordpress-mcp-server/dist/index.js"
      ],
      "env": {
        "WORDPRESS_URL": "https://your-site.com",
        "WORDPRESS_USERNAME": "your-email@example.com",
        "WORDPRESS_APP_PASSWORD": "your-app-password"
      }
    }
  }
}
```

**c) WordPress App Password erstellen:**

1. Gehe zu: `https://your-wordpress-site.com/wp-admin/user-edit.php`
2. Scrolle zu "Application Passwords"
3. Erstelle ein neues Passwort: z.B. "Article Writer Skill"
4. Kopiere das generierte Passwort in `.mcp.json`

### 3. Lokale Claude IDE Konfiguration

**`.claude/settings.local.json`** (im Skill-Verzeichnis):

```json
{
  "enabledMcpjsonServers": [
    "wordpress"
  ],
  "permissions": {
    "allow": [
      "Skill(websnapz-article-writer)"
    ]
  }
}
```

## Verwendung

### Skill starten

```bash
# Im Claude Code / Claude IDE
/websnapz-article-writer
```

### Beispiel: Artikel schreiben

```
Schreib einen Artikel über: "Die beste Schlaf-Routine für Programmierer"
```

Der Skill führt dich durch alle 5 Phasen:

1. **Research** - Thema recherchieren, Referenz-Artikel finden
2. **Outline** - Struktur planen
3. **Content** - Artikel schreiben
4. **Validation** - SEO, Formatierung, Qualität prüfen
5. **WordPress** - Optional: Als Draft hochladen

## Ordner-Struktur

```
Article-Helper-Skill/
├── .mcp.json              # WordPress MCP Config (NICHT committen!)
├── .mcp.json.example      # Vorlage für .mcp.json
├── README.md              # Diese Datei
├── SKILL.md               # Skill-Dokumentation
├── ARCHITECTURE.md        # Technische Architektur
├── phases/                # Phasen-Prompts
│   ├── phase-1-research.md
│   ├── phase-2-outline.md
│   ├── phase-3-content.md
│   ├── phase-4-validation.md
│   └── phase-5-wordpress.md
├── formatting-guide.md    # Design & Formatting Regeln
├── content-design-guide.md # Content Strategy
├── wordpress-integration.md # WordPress MCP Dokumentation
└── Articles/              # Beispiel-Artikel & Vorlagen
```

## Sicherheit

⚠️ **WICHTIG:**

- **`.mcp.json` NICHT mit Credentials committen!**
- Nutze `.mcp.json.example` als Vorlage
- Alle sensiblen Daten gehören in lokale `.mcp.json`
- `.mcp.json` ist bereits in `.gitignore` geschützt

## Troubleshooting

### WordPress MCP verbindet nicht

```bash
# Prüfe:
1. Ist die WORDPRESS_URL korrekt?
2. Existiert der MCP-Server unter dem Pfad?
3. Sind Username & App Password richtig?
```

### Skill wird nicht erkannt

```bash
# Prüfe:
1. Liegt der Ordner im korrekten `.claude/skills/` Verzeichnis?
2. Hat der Ordner die Datei `SKILL.md`?
3. Starte Claude Code neu
```

### Artikel enthalten interne Links zu "mindsnapz.de"

Die Beispiel-Artikel enthalten interne Links zur mindsnapz.de-Website.
Passe diese an deine Website an oder nutze die Artikel als **reine Vorlagen**.

## Nächste Schritte

1. **Konfiguriere deine WordPress-Daten** (falls benötigt)
2. **Teste den Skill** mit einem kurzen Artikel
3. **Passe die Formatierungs-Regeln an** deine Website an
4. **Teile den Skill** mit deinem Team!

## Feedback & Support

Fragen oder Probleme? Öffne ein Issue im Repository oder kontaktiere den Ersteller.

---

## Über diesen Skill

Entwickelt von [mindsnapz.de](https://mindsnapz.de) | [GitHub](https://github.com/DannyyTv/Article-Helper-Skill)

**Viel Erfolg beim Schreiben! ✍️**
