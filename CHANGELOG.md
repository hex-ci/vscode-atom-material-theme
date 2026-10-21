# Change Log

All notable changes to the "Material Theme Revived (Atom Fork)" extension will be documented in this file.

## 2.1.1

### Fixed
- Diff fills no longer drown the comment color: insertion and deletion use the deep end of the palette (`#1B5E20` / `#B71C1C`) instead of a bright tint, so comments inside a change stay readable (1.85–2.20, was 1.22–1.29) while the change itself stays clearly visible (ΔE 22 against the editor background)
- Word-level and line-level fills stay separated (ΔE 13.2 / 12.8), and body text contrast on the fills rises from 6.99 / 7.38 to 10.56 / 11.80
- Removed text is slightly less saturated than before, so added and deleted blocks carry equal weight

### Technical
- README documents the diff overlay fills and why they use deep tints

## 2.1.0

### Changed
- Diff view rebuilt on the palette: insertion and deletion use the theme's green and light red, with a 30% word-level fill over a 12% line-level fill so changed words stand apart from the changed line
- Scrollbar thumb is a neutral gray (`#6A777A`) instead of a background-toned color; the minimap viewport slider derives from it again (VS Code halves the alpha), so the current viewport is visible
- Focus rings (`focusBorder`, `list.focusOutline`, inline chat input, active input option) use the teal accent, so keyboard focus is findable
- Error status bar items use a deeper red (`#D32F2F`) for legible white text
- Diagnostics, search and word-occurrence highlights, debug icons and variables, merge editor, command center, charts, welcome page, chat panel, comments, multi-cursor, keybinding labels and tree rulers follow the palette instead of VS Code's stock colors
- Terminal ANSI bright colors are distinct again from their normal counterparts
- Line numbers, CodeLens and inlay hints raised out of the near-invisible range; `errorForeground` and git-deleted decorations use the light red so text stays readable on dark backgrounds

### Fixed
- `editorOverviewRuler.findMatchForeground` was opaque, which VS Code rejects — the id must stay transparent (`#00BFA5CC`)
- Bracket match border was fully transparent (`#FF000000`) and the overview ruler find-match marker was an off-palette pure blue

### Technical
- 471 workbench color keys, up from 351; every key checked against both the 1.90 and the current VS Code registries, and ids that require transparency are kept translucent

## 2.0.0

### Changed
- Renamed display name to "Material Theme Revived (Atom Fork)" for clearer distinction from the original
- Replaced extension icon with a new geometric "M" design (no longer uses the Atom atom symbol)
- Completely rewritten README with clear fork attribution, color palette reference, and FAQ section
- Updated description to clearly identify this as a community-maintained fork

### Added
- 250+ new workbench colors covering: bracket pair colorization, indent guides, minimap, breadcrumb, notifications, peek view, testing panel, inline chat, notebooks, merge conflicts, status bar items, and more
- 90+ new syntax highlighting rules for: Rust, modern TypeScript/JS features, Python type hints & decorators, JSX attributes, CSS preprocessors (SCSS/Less/Sass), Go, Java, C#, Ruby, PHP, and SQL
- Markdown heading hierarchy with distinct colors for H1/H2/H3
- Semantic scope support for modern TypeScript features (type parameters, decorators, template expressions, generic operators)
- Marketplace `keywords` in `package.json` for discoverability (material, material design, dark theme, atom material theme, atom material syntax)

### Technical
- Updated minimum VS Code engine requirement from `^1.16.0` to `^1.90.0`

## 1.11.0

- Initial release of the fork
