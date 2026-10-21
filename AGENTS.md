# AGENTS.md

Pure-declaration VS Code theme extension: no runtime code, no dependency tree, no build step. The whole product is one hand-authored theme JSON (`themes/atom-material-color-theme.json`) plus the `package.json` manifest. Work here is color/scope editing, not programming — changes are verified by looking at the Extension Development Host, not by tests.

## Layout

- `themes/atom-material-color-theme.json` — everything: ~470 workbench `colors` entries and 108 `tokenColors` rules.
- `package.json` — manifest; `contributes.themes[0]` points at the theme file and its `label` must equal the theme JSON's `name`.
- `samples/` — one file per language (30+) for eyeballing highlighting; excluded from the package.
- `.vscodeignore` — packaging exclusions; keeps dev files out of the `.vsix`.
- `.kilo/kilo.jsonc` — commit-message prompt for the Kilo tool.

## Verify

```sh
python3 -c "import json;json.load(open('themes/atom-material-color-theme.json'))"   # theme JSON is well-formed
npx @vscode/vsce ls                     # dry run: exactly which files would ship
npx @vscode/vsce package                # builds atom-material-theme-revived-<version>.vsix (gitignored)
```

Visual check: open the folder in VS Code, F5 → `Launch Extension` (`.vscode/launch.json`), pick the theme in the Extension Development Host, then open files under `samples/`.

## Release

1. Add a `## <version>` section to `CHANGELOG.md` (Changed / Added / Technical).
2. Bump `version` in `package.json`.
3. Commit — release commits use the bare version as subject (`2.0.4`); feature commits use Conventional Commits with a gitmoji and a `*` bullet body (`fix: update editorHoverWidget foreground color for better visibility`).
4. `git tag v<version>` — existing tags are lightweight and the tag name includes the `v` prefix that the commit subject omits.
5. `npx @vscode/vsce package`.

## Conventions

- Transparency is 8-digit hex (`#0096887a`), never `rgba()`; opaque values are 7-digit hex. Hex casing is mixed — match the neighbouring entries instead of normalizing.
- `colors` is grouped by workbench area and only roughly alphabetical inside a group. Insert a new key next to its area's neighbours, never at the end of the file.
- `tokenColors` rules always use `scope` as an array plus `settings` (`foreground`, sometimes `fontStyle`). Broad bulk rules come first (rule 0 lists ~100 generic scopes), specific overrides later — VS Code applies the later rule, so a new rule belongs after whatever it overrides. The same scope recurs across rules, so grep the scope before adding one to avoid a silent shadow.
- `fontStyle` is used sparingly: italic for comments and markdown italic/quote, bold for markdown bold/H1–H3.
- `semanticHighlighting` is `false` and there is no `semanticTokenColors` — all highlighting comes from TextMate scopes.
- The README palette tables (`#263238` editor background, `#009688` accent, …) are the design reference; introducing a new base color means updating them.

## Pitfalls

- Colour ids are schema-validated at runtime: `colorUtils.ts` rebuilds a JSON schema from every `registerColor` call, so an id your VS Code build does not know reports `Property <id> is not allowed.`, and an id registered with `needsTransparency` rejects opaque values (`This color must be transparent or it will obscure content`). `.vscode/settings.json` only disables remote schema *download*; it does not silence this. Check the Problems panel, and never add an id that exists only in one release — 1.90 has `scm.historyItem*` ids that current builds removed.
- `engines.vscode` is pinned to `^1.90.0`: a key added after 1.90 does nothing for 1.90 users, and a key removed after 1.90 produces warnings for current users. Add only ids present in both trees.
- `.vscodeignore` is the only packaging filter — anything new at the repo root ships unless listed there (that is why `.kilo/` and `AGENTS.md` are excluded). After adding a root-level file, run `npx @vscode/vsce ls`; the expected package is 8 entries: manifest, `[Content_Types].xml`, `changelog.md`, `LICENSE.md`, `readme.md`, `package.json`, the theme file, `icon.png`.
- Only `images/icon.png` ships; `icon.svg` and `screenshot.png` are excluded, and the README renders the screenshot from `raw.githubusercontent.com/…/images/screenshot.png` — renaming or moving it breaks the Marketplace page.
- Three names must stay in sync: `package.json` `displayName`, `contributes.themes[0].label`, and the theme JSON `name`.
- `engines.vscode` is pinned to `^1.90.0`; a color key added to VS Code after 1.90 is ignored for users on 1.90, so confirm a key exists there before adding it.
- Old `.vsix` files sit in the repo root but are gitignored — never edit or rely on them; rebuild with `vsce package`.
