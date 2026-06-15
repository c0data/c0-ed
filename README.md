# C0-ED

Editor extensions for [C0DATA](https://github.com/c0data/c0-cr) — a structured data format using ASCII C0 control codes as delimiters.

## Contents

- **vscode/** — VS Code extension
- **textmate/** — Shared TextMate grammar (used by VS Code, adaptable to Sublime Text, etc.)
- **examples/** — Sample `.c0` files

## VS Code Extension

### Features

**Syntax highlighting** — TextMate grammar that recognizes all 12 C0DATA control picture glyphs and the structures they form.

**Column formatter** — Three modes for tabular data:

| Mode | Example | Description |
|------|---------|-------------|
| Spaced | `␞ Alice ␟ 1502.30 ␟ DEPOSIT` | Aligned columns + breathing room |
| Aligned | `␞Alice ␟1502.30␟DEPOSIT` | Aligned columns, no extra spaces |
| Compact | `␞Alice␟1502.30␟DEPOSIT` | No padding |

**Glyph sets** — Switchable display characters. Files on disk always use standard Unicode Control Pictures; alternate glyphs are a CSS decoration overlay.

Built-in sets:

| Code | Standard | Moon |
|------|----------|------|
| FS | ␜ | ◆ |
| GS | ␝ | ◇ |
| RS | ␞ | ▸ |
| US | ␟ | · |
| SOH | ␁ | ‡ |
| STX | ␂ | ◖ |
| ETX | ␃ | ◗ |
| EOT | ␄ | ■ |
| ENQ | ␅ | § |
| DLE | ␐ | ⧵ |
| ETB | ␗ | ✓ |
| SUB | ␚ | ⇄ |

**Input method** — Type `\gs` then space to insert `␝`. Works for all 12 codes: `\fs`, `\gs`, `\rs`, `\us`, `\soh`, `\stx`, `\etx`, `\eot`, `\enq`, `\dle`, `\etb`, `\sub`. Escape with `\\gs` to get the literal text `\gs`. Also provides autocomplete when typing `\`.

### Commands

| Command | Key | Description |
|---------|-----|-------------|
| C0DATA: Align Columns | `Ctrl+Alt+A` | Spaced column alignment |
| C0DATA: Compact Columns | | Remove all padding |
| C0DATA: Cycle Format Mode | | Cycle through Spaced → Aligned → Compact |
| C0DATA: Switch Glyph Set | | Choose between standard and moon glyphs |
| Format Document | `Shift+Alt+F` | Format using current mode |

### Custom Glyph Sets

Define custom glyph sets in your VS Code `settings.json`:

```json
{
  "c0data.glyphSets": {
    "blocks": {
      "FS": "█",
      "GS": "▌",
      "RS": "▪",
      "US": "│"
    }
  }
}
```

Omitted keys fall back to the standard Control Pictures.

### Install

```sh
cd vscode
npm install
npx tsc -p ./
npx @vscode/vsce package --allow-missing-repository
code --install-extension c0data-0.2.0.vsix --force
```

### File Extensions

`.c0` and `.c0data` are recognized automatically.

## TextMate Grammar

The shared grammar at `textmate/c0data.tmLanguage.json` can be used in any editor that supports TextMate grammars (Sublime Text, TextMate, etc.). It matches both standard Control Pictures and moon glyph characters.

## License

MIT
