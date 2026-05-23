# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

VS Code dark theme extension ("Material Theme Revived (Atom Fork)") based on the original Atom editor's [atom-material-ui](https://github.com/atom-material/atom-material-ui) and [atom-material-syntax](https://github.com/atom-material/atom-material-syntax). Published by `hex-ci` on the VS Marketplace. The entire theme is a single hand-authored JSON file with no build pipeline, no dependencies, and no tests.

This is a **community-maintained fork** of [tobiasalthoff/atom-material-theme](https://marketplace.visualstudio.com/items?itemName=tobiasalthoff.atom-material-theme). Requires VS Code 1.90.0+.

## Design Philosophy

Preserved from the original Atom Material Theme:

- Borders are subtle or invisible; hover effects use gentle brightness shifts rather than color changes
- Teal (`#009688`) is reserved for active indicators and primary action buttons — not used for decorative elements
- All UI colors derive from the official Material Design palette via `md-colors.less`, not arbitrary hex picks
- The theme targets readability with high contrast between syntax colors and the dark blue-grey background

## Common Commands

This repository has no npm scripts, build step, lint command, package dependencies, or automated test suite.

- Validate theme JSON: `python3 -m json.tool themes/atom-material-color-theme.json >/dev/null`
- Launch the Extension Development Host from VS Code: press **F5** and use `Launch Extension`
- Launch from a shell with the VS Code CLI: `code --extensionDevelopmentPath="$PWD"`
- Package a VSIX: `vsce package`
- Publish to the Marketplace: `vsce publish` (requires an Azure DevOps PAT tied to the `hex-ci` publisher)
- Run a single test: not applicable; use targeted manual visual verification by opening one relevant file from `samples/` in the Extension Development Host

## Development Workflow

1. Edit `themes/atom-material-color-theme.json` directly
2. Validate JSON with `python3 -m json.tool themes/atom-material-color-theme.json >/dev/null`
3. Press **F5** in VS Code to launch the Extension Development Host (configured in `.vscode/launch.json`)
4. Visually verify changes against relevant sample files in `samples/` (32 sample files for syntax highlighting coverage)
5. Package with `vsce package` to produce the `.vsix` file
6. Publish with `vsce publish` only when releasing

## Theme Architecture

This extension has no runtime activation code. `package.json` contributes exactly one dark theme through `contributes.themes[0].path`, which points VS Code at `./themes/atom-material-color-theme.json`.

`themes/atom-material-color-theme.json` is the source of truth and has these top-level responsibilities:

- **Theme metadata**: `name`, `type: "dark"`, and `semanticHighlighting: false`
- **`colors`** (351 entries): Workbench/UI chrome colors covering modern VS Code surfaces (activity bar, sidebar, tabs, terminal, status bar, scrollbar, diff editor, git decorations, bracket pair colorization, inline chat, notebooks, testing panel, etc.)
- **`tokenColors`** (108 rules): TextMate scope-based syntax highlighting rules mapping scopes to foreground colors and optional `fontStyle`

`.vscodeignore` controls what ships in the VSIX. Development-only files such as `.vscode/`, `CLAUDE.md`, `samples/`, screenshots, SVG source assets, existing `*.vsix` files, and `node_modules/` are excluded from packaged extensions.

### Color Palette

The theme uses a Material-inspired dark palette anchored to blue-grey backgrounds (`#20292e` - `#273238`) with teal (`#009688`) as the accent color.

**Background hierarchy (dark to light):**
| Color | Hex | Role |
|-------|-----|------|
| Darkest | `#20292e` | Input fields, sidebar headers, dropdowns |
| Dark | `#232e33` | Tabs, sidebar, panels, status bar |
| Base | `#263238` | Editor background |
| Lighter | `#273237` | Terminal background |
| Line highlight | `#212b30` | Active line highlight |

**Syntax colors:**
| Color | Hex | Role |
|-------|-----|------|
| White | `#EEFFFF` | Default text, variables, punctuation |
| Cyan | `#89DDF3` | Operators, braces |
| Green | `#C3E88D` | Strings, property names, headings |
| Orange | `#F78C6A` | Numbers, parameters |
| Red | `#F07178` | HTML/XML tags, language constants |
| Grey-blue | `#4f6875` | Comments (italic) |
| Purple | `#C792EA` | Keywords, storage types |
| Blue | `#82AAFF` | Functions, method calls |
| Yellow | `#FFCB6B` | Classes, types |
| Pink-red | `#FF5370` | `this`, `super`, special variables |
| Teal | `#73d1c8` | CSS property names, object literal keys |
| Muted teal | `#B2CCD6` | Generic tag names |
| Pink | `#ff869a` | Markdown links |

**UI accent colors:**
| Color | Hex | Role |
|-------|-----|------|
| Teal | `#009688` | Primary accent (activity bar, selections, borders) |
| Light teal | `#00BFA5` | Hover states for teal elements |
| Red-400 | `#EF5350` | Errors, deletions, warnings |
| Amber-400 | `#FFCA28` | Warnings, modifications, queued items |
| Light green | `#8BC34A` | Success, additions |
| Blue-300 | `#4FB6F7` | Info, skipped items |

### Material Design Color Mapping

All UI colors follow Google Material Design specifications from [md-colors.less](https://raw.githubusercontent.com/atom-material/atom-material-ui/master/styles/md-colors.less):

- `#009688` = `md-teal-500` (base/accent)
- `#00BFA5` = `md-teal-A700` (hover)
- `#263238` = `md-blue-grey-900` (editor bg)
- `#EF5350` = `md-red-400` (error)
- `#FFCA28` = `md-amber-400` (warning)
- `#8BC34A` = `md-light-green-500` (success)
- `#4FB6F7` = `md-blue-300` (info)

## Key Files

- `themes/atom-material-color-theme.json` - The theme definition (only source file)
- `package.json` - Extension manifest (contributes the theme, no scripts/deps)
- `samples/` - 32 language example files for manual visual testing (not automated tests)
- `images/` - Marketplace icon and screenshot source assets
- `.vscode/launch.json` - F5 Extension Host debug configuration
- `.vscodeignore` - VSIX packaging exclusions

## Conventions

- Minimum VS Code engine: `^1.90.0` (set in `package.json`); bump only when using features from a newer API version
- Theme is hand-authored, not generated from code
- When adding new scope rules, prefer extending existing `tokenColors` entries with additional scope strings rather than creating new rule objects
- Keep the JSON file sorted logically: workbench `colors` first, then `tokenColors` grouped semantically
- Scope strings follow TextMate grammar naming conventions (e.g., `entity.name.type.ts`, `support.class.component.html`)
- Language-specific scopes should include variants for `.js`, `.ts`, `.tsx` where applicable
- **Color consistency**: New workbench colors should use existing palette colors or their transparency variants. Do not introduce new hex values unless they are standard Material Design colors
- **Background depth**: New UI surfaces should fit within the established background hierarchy (`#20292e` to `#273237`)
