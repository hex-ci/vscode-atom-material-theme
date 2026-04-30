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

## Development Workflow

There are no npm scripts or build tools. The workflow is:

1. Edit `themes/atom-material-color-theme.json` directly
2. Press **F5** in VS Code to launch the Extension Development Host (configured in `.vscode/launch.json`)
3. Visually verify changes against sample files in `samples/` (35 language examples for testing syntax highlighting)
4. Package with `vsce package` to produce the `.vsix` file
5. Publish with `vsce publish` (requires Azure DevOps PAT tied to the `hex-ci` publisher)

## Theme Architecture

`themes/atom-material-color-theme.json` has two sections:

- **`colors`** (~350 entries): Workbench/UI chrome colors covering all modern VS Code features (activity bar, sidebar, tabs, terminal, status bar, scrollbar, diff editor, git decorations, bracket pair colorization, inline chat, notebooks, testing panel, etc.)
- **`tokenColors`** (~108 rules): TextMate scope-based syntax highlighting rules mapping scopes to foreground colors and optional fontStyle

`semanticHighlighting` is explicitly set to `false`.

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
- `samples/` - Language example files for visual testing (not automated tests)
- `images/` - Marketplace icon and screenshot
- `.vscode/launch.json` - F5 Extension Host debug configuration

## Conventions

- Minimum VS Code engine: `^1.90.0` (set in `package.json`); bump only when using features from a newer API version
- Theme is hand-authored, not generated from code
- When adding new scope rules, prefer extending existing `tokenColors` entries with additional scope strings rather than creating new rule objects
- Keep the JSON file sorted logically: workbench `colors` first, then `tokenColors` grouped semantically
- Scope strings follow TextMate grammar naming conventions (e.g., `entity.name.type.ts`, `support.class.component.html`)
- Language-specific scopes should include variants for `.js`, `.ts`, `.tsx` where applicable
- **Color consistency**: New workbench colors should use existing palette colors or their transparency variants. Do not introduce new hex values unless they are standard Material Design colors
- **Background depth**: New UI surfaces should fit within the established background hierarchy (`#20292e` to `#273237`)
