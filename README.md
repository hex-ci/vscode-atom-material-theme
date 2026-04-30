# Material Theme Revived (Atom Fork)

> A community-maintained fork of [Atom Material Theme](https://marketplace.visualstudio.com/items?itemName=tobiasalthoff.atom-material-theme) by tobiasalthoff. This extension keeps the beloved Material Design dark theme alive for VS Code with ongoing maintenance and compatibility updates. Requires VS Code 1.90.0+.

<div align="center">
  <a href="https://vscode.dev/theme/hex-ci.atom-material-theme-revived">
    <img src="https://img.shields.io/badge/preview%20in-vscode.dev-blue" alt="Preview in VS Code">
  </a>
  <img src="https://img.shields.io/badge/VS_Code-%3E%3D1.90.0-blue" alt="VS Code 1.90.0+">
</div>

---

## About This Fork

This extension is a **fork** of the original Atom Material Theme, preserved and maintained by the community. The original author [@tobiasalthoff](https://github.com/tobiasalthoff) created an excellent port of the Atom editor's Material UI and Material Syntax themes for VS Code. This fork exists to ensure the theme remains available and compatible with current versions of VS Code.

### What Makes This Fork Different

- **Community maintained** — actively updated for VS Code compatibility
- **Same beloved look** — retains the exact Material Design palette from the original
- **Design philosophy preserved** — borders are subtle or invisible, hover effects use gentle brightness shifts, and teal is reserved for active indicators and primary action buttons
- **Enhanced workbench colors** — 250+ additional UI colors covering bracket pair colorization, indent guides, minimap, notifications, testing panel, inline chat, and more
- **Expanded syntax highlighting** — 90+ new token rules for Rust, modern TypeScript/JS, Python type hints, JSX attributes, CSS preprocessors, Go, Java, C#, Ruby, PHP, and SQL
- **No extra complexity** — still a single, hand-authored theme file with zero dependencies

## Preview

![Theme Preview](https://raw.githubusercontent.com/hex-ci/vscode-atom-material-theme/main/images/screenshot.png)

## Color Palette

This theme uses a carefully curated dark Material palette with a consistent background hierarchy:

### Background Hierarchy

| Layer | Hex Code | Usage |
|-------|----------|-------|
| Darkest | `#20292e` | Input fields, sidebar headers, dropdowns |
| Dark | `#232e33` | Tabs, sidebar, panels, status bar |
| Base | `#263238` | Editor background |
| Lighter | `#273237` | Terminal, panel backgrounds |
| Hover | `#2c383d` | Hover states, active selections |

### Syntax Colors

| Role | Hex Code |
|------|----------|
| Default text | `#EEFFFF` |
| Comments (italic) | `#4f6875` |
| Strings | `#C3E88D` |
| Keywords | `#C792EA` |
| Functions | `#82AAFF` |
| Classes/Types | `#FFCB6B` |
| Numbers | `#F78C6A` |
| HTML Tags | `#F07178` |
| Operators | `#89DDF3` |
| Accent (teal) | `#009688` |
| `this` / `super` | `#FF5370` |

### UI Accent Colors

| Role | Hex Code |
|------|----------|
| Error / Deletion | `#EF5350` |
| Warning / Modification | `#FFCA28` |
| Success / Addition | `#8BC34A` |
| Info | `#4FB6F7` |
| Teal hover | `#00BFA5` |

## Quick Install

1. Open **Extensions** (`Ctrl+Shift+X` / `Cmd+Shift+X`)
2. Search for **Material Theme Revived**
3. Click **Install**
4. Select the theme: **File** > **Preferences** > **Color Theme** > **Material Theme Revived (Atom Fork)**

## Recommended Editor Settings

For the best reading experience with this theme, try these settings in your `settings.json`:

```jsonc
{
  "editor.fontSize": 16,
  "editor.lineHeight": 1.5,
  "editor.letterSpacing": 0.5
}
```

## Supported Languages

Syntax highlighting covers 30+ languages including:

- **Web**: JavaScript, TypeScript, JSX/TSX, HTML, CSS, SCSS, Less, Sass
- **Backend**: Python, Ruby, Rust, Go, Java, C#, SQL, PHP, Perl
- **Data**: JSON, YAML, Markdown, XML, GraphQL
- **Mobile**: Objective-C
- **Others**: Shell scripts, INI config files, CoffeeScript

## FAQ

### Is this the original Atom Material Theme?

No. This is a **community fork**. The original was created by [@tobiasalthoff](https://github.com/tobiasalthoff) and ported the [atom-material-ui](https://github.com/atom-material/atom-material-ui) and [atom-material-syntax](https://github.com/atom-material/atom-material-syntax) themes from the Atom editor to VS Code. This fork preserves the same visual design while keeping it maintained.

### Why a fork?

The original extension may no longer be actively maintained. This fork ensures the theme remains available and compatible with the latest versions of VS Code.

## Contributing

Found a scope that isn't highlighted correctly? Have a suggestion?

- **Issues**: Report bugs or missing language support on [GitHub](https://github.com/hex-ci/vscode-atom-material-theme/issues)
- **Pull Requests**: The theme is a single JSON file — feel free to propose scope additions or color tweaks

## Credits

- **Original theme**: [Atom Material Theme](https://marketplace.visualstudio.com/items?itemName=tobiasalthoff.atom-material-theme) by [@tobiasalthoff](https://github.com/tobiasalthoff)
- **Source projects**: [atom-material-ui](https://github.com/atom-material/atom-material-ui) and [atom-material-syntax](https://github.com/atom-material/atom-material-syntax)
- **Sample files**: [Atom Language Examples](https://github.com/atom/language-examples)

## License

See [LICENSE.md](LICENSE.md). The original Atom Material Theme was created by tobiasalthoff. This fork is maintained by Hex.
