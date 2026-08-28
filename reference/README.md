# Reference

Upstream artefacts, kept here to write themes against. None of them is a theme
of this repository and none is meant to be installed. Only this file is
tracked; the copies themselves are ignored (`reference/` in `.gitignore`) and
are refreshed by hand from the sources listed below.

## Documentation

Two documents from the Super Productivity repository. Copies live here so a
question can be answered offline and with `grep`; the links are authoritative
and win over the copy whenever the two disagree.

| File | Upstream | What it settles |
| --- | --- | --- |
| `theming-contract.md` | [docs/theming-contract.md](https://github.com/super-productivity/super-productivity/blob/master/docs/theming-contract.md) | The public contract a custom theme fills: the four required tokens, the recommended and optional ones, and which selector each must be declared on. |
| `styling-guide.md` | [docs/styling-guide.md](https://github.com/super-productivity/super-productivity/blob/master/docs/styling-guide.md) | The app's own design tokens — spacing, type scale, z-index, transitions, breakpoints, focus ring — and the conventions its components follow. |

### What to look up where

`theming-contract.md`:

- [Required tokens](https://github.com/super-productivity/super-productivity/blob/master/docs/theming-contract.md#required-tokens) — `--surface-1`, `--surface-2`, `--ink`, `--ink-on-channel`.
- [Recommended](https://github.com/super-productivity/super-productivity/blob/master/docs/theming-contract.md#recommended-tokens) and [optional tokens](https://github.com/super-productivity/super-productivity/blob/master/docs/theming-contract.md#optional-tokens) — the rest of the surface ladder and the ink ramp; the `--state-*-alpha` scalars.
- [Special tokens](https://github.com/super-productivity/super-productivity/blob/master/docs/theming-contract.md#special-tokens) — `--ink-on-channel` as an RGB triplet, and the bridge from the legacy `--*-bg-opacity` names.
- [Selector contract](https://github.com/super-productivity/super-productivity/blob/master/docs/theming-contract.md#selector-contract) — why primitives must sit on `body` / `body.isDarkTheme` and never on `:root`.
- [Validation rules](https://github.com/super-productivity/super-productivity/blob/master/docs/theming-contract.md#validation-rules) — the hard rejects at install time: remote or relative `url(...)`, `@import`, `image()` / `image-set()`, over 500 KB.

`styling-guide.md`:

- [Typography scale](https://github.com/super-productivity/super-productivity/blob/master/docs/styling-guide.md#typography-scale) and [spacing variables](https://github.com/super-productivity/super-productivity/blob/master/docs/styling-guide.md#spacing-variables-8px-grid) — `--font-size-*` and the 8px `--s*` grid.
- [Colour variables](https://github.com/super-productivity/super-productivity/blob/master/docs/styling-guide.md#color-variables) — the semantic names the components read, and what the light and dark themes set them to.
- [Transitions](https://github.com/super-productivity/super-productivity/blob/master/docs/styling-guide.md#transitions--animations), [z-index](https://github.com/super-productivity/super-productivity/blob/master/docs/styling-guide.md#z-index-layers), [layout](https://github.com/super-productivity/super-productivity/blob/master/docs/styling-guide.md#layout-variables) and [breakpoints](https://github.com/super-productivity/super-productivity/blob/master/docs/styling-guide.md#responsive-breakpoints) — the ladders to reuse rather than restate.
- [Authoring themes](https://github.com/super-productivity/super-productivity/blob/master/docs/styling-guide.md#authoring-themes) — including the one hard rule about `magic-side-nav`: no `backdrop-filter`, `filter`, `transform` or `contain` on the host, or the mobile drawer never appears. Put them on the inner `.nav-sidenav`.
- [Utility classes](https://github.com/super-productivity/super-productivity/blob/master/docs/styling-guide.md#utility-classes) and [global component styles](https://github.com/super-productivity/super-productivity/blob/master/docs/styling-guide.md#global-component-styles) — what already exists before a new selector is written.

## Stylesheets

| File | Upstream | Why it is here |
| --- | --- | --- |
| `dark-base.css` | [src/assets/themes/dark-base.css](https://github.com/super-productivity/super-productivity/blob/master/src/assets/themes/dark-base.css) | The shortest complete example of the contract in practice: surface ladder, ink, separators, and the component variables that follow from them. The three themes in this repository follow its declaration order. |
| `arc.css` | [src/assets/themes/arc.css](https://github.com/super-productivity/super-productivity/blob/master/src/assets/themes/arc.css) | A second shipped theme, for comparison where `dark-base.css` leaves a token unstated. |
| `core-styles.css` | Not on GitHub — extracted from the packaged app (`resources/app.asar`, Super Productivity 18.16.0) | The app's global stylesheet, where the contract is actually written: `--task-c-bg: var(--surface-2)`, the spacing and radius scales, the Material token defaults. Minified but greppable, and it settles what guessing from the DOM cannot. |

The other shipped themes are in the same directory upstream:
[src/assets/themes/](https://github.com/super-productivity/super-productivity/tree/master/src/assets/themes).

## Refreshing

```sh
base=https://raw.githubusercontent.com/super-productivity/super-productivity/master
curl -sSL -o reference/theming-contract.md "$base/docs/theming-contract.md"
curl -sSL -o reference/styling-guide.md    "$base/docs/styling-guide.md"
curl -sSL -o reference/dark-base.css       "$base/src/assets/themes/dark-base.css"
curl -sSL -o reference/arc.css             "$base/src/assets/themes/arc.css"
```

`core-styles.css` has no such source; it is replaced by unpacking the app again
after an upgrade, and the version it came from belongs in the table above.
