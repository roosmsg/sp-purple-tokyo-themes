# Purple Tokyo

A light/dark theme pair for [Super Productivity](https://github.com/super-productivity/super-productivity), plus a set of interface changes that go with it.

- **Dark — Shades of Purple (Super Dark):** deep indigo surfaces, white text, a muted violet for supporting text, Claude salmon as the accent.
- **Light — Tokyo Light:** cool blue-grey surfaces, ink-blue text, Tokyo Night Light's blue as the accent.

Both palettes are taken from Personal Work Manager and remapped onto Super Productivity's [theming contract](https://github.com/super-productivity/super-productivity/blob/master/docs/theming-contract.md): the surface ladder and the ink primitives drive the semantic tokens, so most of the app follows from the two colour blocks at the top of the file. The rest covers the tokens the base pins to a neutral grey ramp that the ladder does not reach.

## Install

Settings → General → Theme → **Install theme…**, then pick `purple-tokyo.css`. The file is stored locally in IndexedDB; nothing leaves the machine. Re-uploading a file with the same name overwrites the previous version.

The picker labels a theme after its filename, so rename the file if you want a different name in the list.

## What it changes beyond colour

Each section in the file stands on its own and can be deleted without touching the rest.

| Section | What it does |
| --- | --- |
| Typography | IBM Plex Sans for the interface, JetBrains Mono for code. Includes an override for Material's components, which compile their own font family and never read the variable. |
| Side nav | The buttons in the Projects and Tags headers, and the headings themselves, stay out of sight until the row is hovered or holds keyboard focus. The Help entry is removed. Hover lights the whole row rather than the label alone. |
| Action bar | In both the horizontal and experimental vertical layout, every button except Play and Add task stays visible at 25% opacity until the bar is hovered or holds keyboard focus. Both layouts wait 2 seconds before dimming again after hover. |
| Flat surfaces | Task rows separate with a hairline instead of a drop shadow. |
| Material surfaces | Menus, dialogs, dropdowns, the date picker, cards and the snackbar take the theme's own surfaces instead of Material's grey. Tooltips stay deliberately contrasting. |
| Today icon | Replaces the sun with a bolt on the today affordances. |
| Planner icon | Uses the built-in Material Symbols `next_week` glyph for Planner in the left navigation. |
| Schedule icons | Uses the built-in Material Symbols `calendar_clock` glyph for Schema in the left navigation and `pending_actions` on its right-panel button in desktop and mobile layouts. |
| Empty state | Hides the horizon drawing under "no tasks planned" and keeps the heading clear of the add-more button. |
| Task work view | Makes task lists, empty states and the finish-day action larger than Settings. |
| Dashboard icon | Gives the Dashboard plugin entry in the left menu the built-in Material Symbols `avg_pace` glyph in the same muted colour as Schema; no SVG asset is added. |
| Window controls | Places a compact theme surface behind Electron's native minimise, maximise and close buttons, matching the Windows reference while preserving native behaviour. Its dimensions follow Electron's native title-bar safe area, so Ctrl + scroll does not enlarge it. When the experimental vertical action bar is enabled, the rail starts directly below this surface and preserves the original Play position through internal top padding. |
| Chrome scale | Puts the two navigation rails a step below the content in size. |

## Tuning

- `--today-icon` — the Material Symbols ligature drawn in place of the sun. `bolt` by default; `electric_bolt`, `offline_bolt`, `flash_on` and `thunderstorm` are the other candidates in the app's icon picker.
- `--planner-nav-icon` — the Material Symbols ligature used for Planner in the left navigation (`next_week`).
- `--schedule-nav-icon` and `--schedule-panel-icon` — the Material Symbols ligatures used for Schema in the left navigation (`calendar_clock`) and on the right-panel control (`pending_actions`).
- `--work-view-scale` — the task work view relative to Settings (`1.1`). This follows the effect of one extra Ctrl + scroll step without changing Settings itself.
- `--side-nav-scale`, `--nav-footer-scale`, `--action-bar-scale` — the navigation scale in three places: the left rail (`1.05`), the search/timeline/settings group at the foot of that rail relative to the rail itself (`1`, matching the other rail buttons), and the right action strip (`0.85`). `--action-bar-idle-opacity` (`0.25`) dims every action-bar button except Play and Add task by 75% while the bar is idle, in both desktop layouts. `--action-bar-hover-out-delay` (`2s`) delays both layouts' return to idle opacity. `--play-button-size` (`46px`) sets the time-tracking button apart from the vertical strip scale; the strip widens to fit it.
- `--window-controls-width` (`138px`) is the fallback width when Electron does not expose its native title-bar safe area; `--window-controls-bg` controls the backing strip's colour.
- `--vertical-action-bar-play-padding-top` (`12px` with the app's default spacing tokens) keeps Play separated from the native controls while the rail background starts at the top.

## Notes

- Themes installed through Settings cannot load external assets — no remote URLs, no `@import`, no bundled font files. The font stack therefore only names fonts that are installed on the machine.
- One selector keys off the Dutch button title `Voeg toe aan Mijn Day`, because that button carries no distinguishing class. With the interface in another language that line needs the string from that language.
- Setting the primary palette means per-project and per-tag colours no longer tint the interface. Delete the primary ladders and the accent block to hand that role back.
