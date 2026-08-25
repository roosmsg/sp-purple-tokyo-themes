# Purple Tokyo

A light/dark theme pair for [Super Productivity](https://github.com/super-productivity/super-productivity), plus a set of interface changes that go with it.

- **Dark — Shades of Purple (Super Dark):** deep indigo surfaces, white text, a muted violet for supporting text, Claude salmon as the accent.
- **Light — Tokyo Light:** cool blue-grey surfaces, ink-blue text, Tokyo Night Light's blue as the accent.

Both palettes are taken from Personal Work Manager and remapped onto Super Productivity's [theming contract](https://github.com/super-productivity/super-productivity/blob/master/docs/theming-contract.md): the surface ladder and the ink primitives drive the semantic tokens, so most of the app follows from the two colour blocks at the top of the file. The rest covers the tokens the base pins to a neutral grey ramp that the ladder does not reach.

## Variants

Two further files pair the same interface changes with other palettes from Personal Work Manager. Everything below the two colour blocks is identical in all three, so a change to one section has to be repeated in the others; Super Productivity's installer accepts a single self-contained file and no `@import`, which is why the shared part is copied rather than referenced.

| File | Light slot | Dark slot |
| --- | --- | --- |
| `purple-tokyo.css` | Tokyo Light | Shades of Purple (Super Dark) |
| `paper-purple.css` | Licht — white and near-white zinc surfaces, sky blue accent | Shades of Purple (Super Dark) |
| `purple-tokyo-night.css` | Shades of Purple — indigo surfaces, white text, salmon accent | Tokyo Night — near-black blue surfaces, pale blue text, the theme's blue accent |

`purple-tokyo-night.css` puts a dark palette in the light slot, as asked. Shades of Purple is a dark theme in Personal Work Manager as well; it is the lighter of the two purples, not a light theme. Switching modes therefore moves between two dark looks rather than between light and dark, and Super Productivity still treats the light slot as light mode — its drop shadows and the platform's `color-scheme` for native widgets are the light-mode ones.

## Install

Settings → General → Theme → **Install theme…**, then pick the `.css` file you want. It is stored locally in IndexedDB; nothing leaves the machine. Re-uploading a file with the same name overwrites the previous version. Installing more than one file puts all of them in the list.

The picker labels a theme after its filename, so rename the file if you want a different name in the list.

## What it changes beyond colour

Each section in the file stands on its own and can be deleted without touching the rest.

| Section | What it does |
| --- | --- |
| Typography | Inter throughout except the view title, which keeps the app's own stack; Inter is the face PWM uses (falling back to the app's own stack where Inter is not installed), JetBrains Mono for code. Includes an override for Material's components, which compile their own font family and never read the variable, and keeps the plugin security warning at normal body weight. |
| Side nav | The buttons in the Projects and Tags headers, and the headings themselves, stay out of sight until the row is hovered or holds keyboard focus. The Help entry is removed. Hover lights the whole row rather than the label alone. |
| Action bar | In both the horizontal and experimental vertical layout, every button except Play and Add task stays visible at 25% opacity until the bar is hovered or holds keyboard focus. Both layouts wait 2 seconds before dimming again after hover. |
| Flat surfaces | Task rows separate with a hairline instead of a drop shadow. |
| Material surfaces | Menus, dialogs, dropdowns, the date picker, cards and the snackbar take the theme's own surfaces instead of Material's grey. Tooltips stay deliberately contrasting. Segmented controls such as the dark-mode switch drop Material's grey for the theme's own surfaces. |
| Today icon | Replaces the sun with a bolt on the today affordances. |
| Planner icon | Uses the built-in Material Symbols `next_week` glyph for Planner in the left navigation. |
| Schedule icons | Uses the built-in Material Symbols `calendar_clock` glyph for Schema in the left navigation and `pending_actions` on its right-panel button in desktop and mobile layouts. |
| Empty state | Hides the horizon drawing under "no tasks planned", adds `48px`-equivalent breathing room above the heading and keeps an explicit `32px`-equivalent gap before the add-more button. |
| Content scale | Keeps task lists, empty states and the finish-day action at their existing `1.1` scale while zooming the desktop Settings page out to `0.9`. |
| Dashboard icon | Gives the Dashboard plugin entry in the left menu the built-in Material Symbols `avg_pace` glyph in the same muted colour as Schema; no SVG asset is added. |
| Window controls | Places a compact theme surface behind Electron's native minimise, maximise and close buttons, matching the Windows reference while preserving native behaviour. Its dimensions follow Electron's native title-bar safe area, so Ctrl + scroll does not enlarge it. When the experimental vertical action bar is enabled, the rail starts directly below this surface and preserves the original Play position through internal top padding. |
| Square hover states | Squares every rounded hover highlight: icon-button circles, task rows, side-nav rows and links, and list and option rows. The right-hand action bar and the settings tabs keep their rounded shape; round controls, pills and button fills keep theirs. |
| Inline task tags | Puts the project and tags on the task line instead of under it, separated by a hairline; long titles still wrap them to the next line. |
| Task text | Sets the task name as PWM does: Inter at 14px on a 20px line, regular weight, in the primary ink, and holds that weight and leading while the line is being edited. A finished name takes the muted ink through `--task-done-ink`, on top of the app's own strike-through and fade. |
| Task row controls | Play and the detail-panel toggle drop from 24px to 20px, and play takes the theme accent. |
| Plugin manager | Rebalances the plugin cards: a 26px icon, a 20.5px name, and descriptions, metadata and labels in muted ink at 15.5px with looser leading. |
| Compact menus | Brings the task context menu to 40px rows, a 12.5px label and 17px icons, tightens the tag, project and estimate submenus to 32px rows in regular weight, and squares the icon strip at its head with 23px glyphs. |
| Text rendering | Restores Windows subpixel rendering, which Material and the app switch off with `-webkit-font-smoothing: antialiased`. Icon faces keep greyscale smoothing. Bold type caps at SemiBold and inline emphasis at Medium, with table and section headers a step smaller. |
| Chrome scale | Puts the two navigation rails a step below the content in size. |

## Lucide icons

These themes draw the app's own icons by substitution: the ligature the icon font would have rendered is hidden and a different one is written in its place — a bolt where the sun was, and so on. That works because a Material icon is text.

If the [Lucide Icons plugin](https://github.com/roosmsg/super-productivity-lucide-icons) is installed, the whole interface is drawn in Lucide instead, and the substitutions above still hold: the plugin reads the ligature a theme has asked for and draws the Lucide equivalent, so the bolt arrives as Lucide's `zap` rather than as a Material glyph among Lucide ones. Nothing here needs changing for that to happen.

Two hooks are there for rules that should apply only when the plugin is drawing:

| Selector | Matches |
| --- | --- |
| `html[data-lucide-icons]` | anything, while the plugin is active — it removes the attribute when disabled |
| `mat-icon[data-lucide-icon="play_arrow"]` | one replaced icon, named by the Material ligature it stands in for |

The drawing itself lives in that element's `::after`, as a mask. A rule of your own that puts a mask there is left alone by the plugin, which is how a theme keeps an icon the plugin would otherwise replace.

## Tuning

- `--today-icon` — the Material Symbols ligature drawn in place of the sun. `bolt` by default; `electric_bolt`, `offline_bolt`, `flash_on` and `thunderstorm` are the other candidates in the app's icon picker. All five are carried by the Lucide plugin, so any of them still arrives as a bolt — Lucide's `zap`, or `cloud-lightning` for `thunderstorm` — rather than as a Material glyph among Lucide ones.
- `--icon-scale` — how large the Lucide plugin draws an icon, as a multiple of the size a glyph would have been. `0.92` by default; `1` is the app's own figure. It sits inside the plugin section and does nothing without it, since the icon font needs no such adjustment: a glyph is drawn at the element's font-size, while a mask fills whatever it is given, and the app states the two differently in places. Boxes do not move, so this shifts no layout.
- `--icon-scale-tasks` — the same figure for the task list, the view around it and the task detail panel, where an icon sits beside 14px text rather than beside a label in a rail or a menu. `0.8`. It is applied by redefining `--icon-scale` on those containers, so it reaches every icon inside them through inheritance rather than through a selector that has to know the markup.
- `--planner-nav-icon` — the Material Symbols ligature used for Planner in the left navigation (`next_week`).
- `--schedule-nav-icon` and `--schedule-panel-icon` — the Material Symbols ligatures used for Schema in the left navigation (`calendar_clock`) and on the right-panel control (`pending_actions`).
- `--schedule-time-size` (`12.5px`) and `--schedule-marker-size` (`11.5px`) — the hours down the side of Schema and the two work markers in the same gutter. The app sets them at 11.2px and 10px, and the view scale takes a further fifth off both; these are the labels the whole grid is read against, so they get more than it back. Like `--schedule-title-size` below, both are stated at the size they are to be *read* at and divided by the scale, so zooming the view out again does not quietly shrink them along with it.
- `--detail-panel-icon-size` (`20px`) — the icons in the task detail panel, which stand beside short labels in a narrow column where the 24px the task list uses is more than the panel needs. Only the drawing steps down; the 24px box stays, so the rows keep their rhythm.
- `--work-view-scale`, `--settings-view-scale` and `--schedule-view-scale` — independent scales for the task work view (`1`), the desktop Settings page (`0.95`) and Schema (`0.8`), which is the view that most wants more hours and days on screen at once. Adjusting one does not change the others. All three use `zoom`, which is a layout property, so the view really is smaller and lays out to the room it now has rather than being drawn smaller and clipped. Settings and Schema are held to the desktop; on a narrow window both are already tight.
- `--schedule-title-size` (`18px`) — the size the week heading in Schema is *read* at, not the size it is set at: the rule divides it by `--schedule-view-scale`, which the zoom then multiplies straight back out. Move the scale and the heading stays exactly where it is, with no second number to keep in step. The app's own page title — the word Schema in the header — sits outside the scaled element and never needed the correction.
- `--task-project-size` (`1.45em`) and `--task-project-icon-size` (`1.35em`) — the project on the task line, which reads as a heading for that line rather than as another chip on it, so it is set above the tags that follow. The icon is sized with the text, since one without the other leaves the icon looking like a leftover. Both are stated sizes, so the icon hands `--icon-scale` back to `1` and comes out the same in the icon-font build and with the Lucide plugin.
- `--play-button-hover-scale` (`1.06`) and `--play-button-hover-layer-opacity` (`0.12`) — the play button in the right action bar answers the pointer by growing slightly and deepening Material's own hover layer, whose default `0.04` is a figure meant for a large flat surface rather than a 46px circle. The growth is dropped for anyone who has asked the system for reduced motion, and neither applies while the button is disabled — which is how it sits when no task is selected.
- `--side-nav-scale`, `--nav-footer-scale`, `--action-bar-scale` — the navigation scale in three places: the left rail (`1.05`), the search/timeline/settings group at the foot of that rail relative to the rail itself (`1`, matching the other rail buttons), and the right action strip (`0.85`). `--action-bar-idle-opacity` (`0.25`) dims every action-bar button except Play and Add task by 75% while the bar is idle, in both desktop layouts. `--action-bar-hover-out-delay` (`2s`) delays both layouts' return to idle opacity. `--play-button-size` (`46px`) sets the time-tracking button apart from the vertical strip scale; the strip widens to fit it.
- `--font-body-stack` and `--font-heading-stack` — the interface face. Both resolve to Inter, the face Personal Work Manager uses; install it (PWM carries `InterVariable.woff2`/`.ttf` under `src/renderer/public/fonts/`) or the stack falls back to Super Productivity's own default. Point `--font-heading-stack` at another family to set headings apart again.
- `--bold-font-weight` and `--emphasis-font-weight` — the caps applied to bold type (`600`) and to inline emphasis (`500`). Set both to `700` for the app's own weights.
- `--body-font-weight` — the interface weight (`400`). Raise to `500` if body copy still reads thin on this display; Inter carries a real Medium, so nothing is synthesised.
- `--window-controls-width` (`138px`) is the fallback width when Electron does not expose its native title-bar safe area; `--window-controls-bg` controls the backing strip's colour.
- `--vertical-action-bar-play-padding-top` (`12px` with the app's default spacing tokens) keeps Play separated from the native controls while the rail background starts at the top.

## Notes

- Themes installed through Settings cannot load external assets — no remote URLs, no `@import`, no bundled font files. The font stack therefore only names fonts that are installed on the machine.
- One selector keys off the Dutch button title `Voeg toe aan Mijn Day`, because that button carries no distinguishing class. With the interface in another language that line needs the string from that language.
- Setting the primary palette means per-project and per-tag colours no longer tint the interface. Delete the primary ladders and the accent block to hand that role back.
