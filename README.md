# Super Productivity themes

Three light/dark theme pairs for [Super Productivity](https://github.com/super-productivity/super-productivity), each a self-contained CSS file installed from the app's own theme picker. All three carry the same set of interface changes, except where a row below names a file, and differ in the palette they put in the light and the dark slot.

| File | Light slot | Dark slot |
| --- | --- | --- |
| `shades-of-purple.css` | Shades of Purple — indigo surfaces, white text, a muted violet for supporting text, salmon as the accent | Shades of Purple taken deeper — near-black indigo, the same white text and salmon accent |
| `paper-purple.css` | Licht — white and near-white zinc surfaces, salmon as the accent | Shades of Purple |
| `minimal-tokyo.css` | Tokyo Light — cool blue-grey surfaces, ink-blue text | Tokyo Night — near-black blue surfaces, pale blue text |

The palettes are remapped onto Super Productivity's [theming contract](https://github.com/super-productivity/super-productivity/blob/master/docs/theming-contract.md): the surface ladder and the ink primitives drive the semantic tokens, so most of the app follows from the two colour blocks at the top of each file. The rest covers the tokens the base pins to a neutral grey ramp that the ladder does not reach.

## Install

Settings → General → Theme → **Install theme…**, then pick the `.css` file you want. It is stored locally in IndexedDB; nothing leaves the machine. Re-uploading a file with the same name overwrites the previous version. The app keeps that stored copy and does not read the file again, so after editing a theme on disk, install it again to see the change. Installing more than one file puts all of them in the list.

The picker labels a theme after its filename, so rename the file if you want a different name in the list.

## What it changes beyond colour

Each section in the file stands on its own and can be deleted without touching the rest. Everything below applies to all three files in both modes unless the row says otherwise. The variables a section exposes are documented at the head of that section in the CSS.

### Navigation and chrome

| Change | What it does |
| --- | --- |
| Side nav | The Projects and Tags headings and their buttons stay out of sight until the header block is hovered or focused, then come up together. Hover lights the whole row. Help leaves the fold-out menu for a square icon button at the end of the Settings row. |
| Active My Day and Inbox | Those two rows keep their own icon colour when open instead of being repainted with the active text colour. |
| Action bar | Every button except Play rests at 20% opacity in dark mode and 30% in light (`--action-bar-idle-opacity`); each comes up on its own, under the pointer or on focus. Add task rests at 18% (`--add-task-idle-opacity`) in `shades-of-purple.css` and `paper-purple.css`; in `minimal-tokyo.css` it stays at full strength. |
| Play button | `minimal-tokyo.css` only. The disc under the play triangle does not take the colour of the project or tag; it is painted from body ink (`--play-button-bg`). |
| Play button opacity | Both modes, all three files. The whole button rests below full and comes to full under the pointer or on focus. Idle — a task to start, none running — is 0.65 on the dark page, 0.75 in `minimal-tokyo.css`; on the light page 0.95 in `paper-purple.css`, 0.92 in `minimal-tokyo.css`, 0.8 in `shades-of-purple.css`. While a timer runs it holds at 0.75 in dark and at each file's own light figure in light (`--play-button-idle-opacity`). |
| Add task glyph | `minimal-tokyo.css` and `paper-purple.css`. The plus is painted from body ink rather than the project colour: a step off the ink at rest, the full ink under the pointer or on focus. |
| Top bar autohide | Vertical rail off, from 600px up. The whole action row waits at zero opacity until the pointer reaches it or focus enters. |
| Play at the end of the row | Vertical rail off. Play moves from the head of the action row to its far end; Add task stays where it was. |
| Vertical rail | The rail is narrowed and meets the strip behind the window controls in a rounded shoulder carrying a hairline. |
| Window controls | A compact strip in a theme surface behind Electron's native buttons, sized from the native title-bar safe area so Ctrl + scroll does not enlarge it. |
| Right panel clearance | The right panel starts below the native window controls instead of opening underneath them. |
| Chrome scale | The two navigation rails sit a step below the content in size. |
| Square hover states | Square hover highlights on the left menu rows only; Material's own shapes stand everywhere else. |
| Project icon | An open project keeps its own colour on its icon in the left menu instead of taking the active text colour. |

### Task list

| Change | What it does |
| --- | --- |
| Flat surfaces | Task rows separate with a hairline instead of a drop shadow. |
| Task text | Inter at 14px on a 20px line, regular weight, in the primary ink, held while the line is edited; a finished name takes the muted ink. |
| Task row controls | Play and the detail-panel toggle drop from 24px to 20px, and play takes the accent. |
| Title fills its line | A task name spans its whole line, so a click anywhere along it opens the name for editing. |
| Finished task hover | A finished row's hover edge is dimmer than an open row's, so a faded row is marked without being lifted. |
| Section tags | Each work-view section heading sits on a small tag in the chrome colour, with the picture blurred behind it. |
| Section arrows | The chevron before a heading points right when the section is closed and down when it is open. |
| Section menu button | The three-dot menu on a backlog heading rests at the action row's idle opacity instead of hiding until the section is hovered. |
| Section rule animation | The line under a heading is the width of the text while the section is closed and grows to the full column when it opens. |
| Add to Today panel | "Add to Today" and "Add more" take the same solid tag as the section headings. |
| Add task pop-up | The floating bar opens further down the page and is centred on the task column rather than on the window, and as wide as that column. |
| Backlog toggle | The round button on the split between the list and the backlog keeps a fixed label colour rather than following the context. |
| Empty state | The horizon drawing under "no tasks planned" is hidden and the heading gets room above and below. |
| Work view status bar | One clock at the head of the line, the duplicate on the middle reading dropped, and the three readings separated by a dot. |
| Estimate remaining | The hourglass glyph after the figure is removed; the label and the number carry the item. |
| Title buttons | The project menu and the filter toggle beside the page title rest at the action row's idle opacity and lift on hover or focus. |

### Task detail panel

| Change | What it does |
| --- | --- |
| Panel surface | The panel takes the rail's surface instead of staying transparent, so the list no longer shows through it, and the hairline down its edge is gone. |
| Task title underline | The 2px primary line under the title is removed, along with the rounding that bent it up at both ends. |
| Detail panel cards | The joins between cards are one flat, inset hairline and Material's own panel borders are gone, so one kind of line runs between fields. |
| Notes weight | Notes, checklists and every inline-markdown field sit at body weight instead of Material's 500. |

### Summary and planner

| Change | What it does |
| --- | --- |
| Finish Day | The Finish Day button, and "Move completed tasks to archive" beside it, take the section-tag shape: quiet surface, hairline, 8px radius, a heavier label. |
| Finish the day | The primary button that closes the summary page takes that shape too, and answers hover with a lift instead of Material's white wash. |
| Summary cards | "Time spent today by tag" and the day-end note sit on a card instead of on the bare page. |
| Summary tabs | The tab strip is an edge-to-edge band in the row surface, no rim and no rounding. The Settings tabs are untouched. |
| Add tasks from today | The outline button on the plan-tomorrow tab takes the Finish Day treatment. |
| Planner day cards | A day column sits on a card instead of a bare column with a line down its start edge. |

### Surfaces and background

| Change | What it does |
| --- | --- |
| Page backdrop | Light mode loses the two primary-tinted glows the app paints behind the page; dark mode keeps its wash. |
| Disabled background tint | `minimal-tokyo.css` only. Where a context's "Disable background tint" box is ticked, the colours the app still fills from that context become body ink. |
| Hairlines | `minimal-tokyo.css`, dark mode only. Separators and dividers are a share of body ink mixed into the page rather than stated border colours, which sit high on near-black surfaces. |
| Fading rules | A rule fades out instead of stopping dead. |
| Panel seams | `minimal-tokyo.css` only. The three full-height lines the side panels draw against the page are set to zero width; surface colour separates the columns. |
| Wallpaper veil | Dark mode. The darkening of a background image splits into a fixed floor on the picture itself and the app's own veil over it. |
| Settings backdrop | No glow behind the page, and no wallpaper at all, on the Settings, Search, Upcoming, Schedule and plugin pages. |
| Placeholder wallpaper | A project or tag whose picture is set to `https://` or `null` shows no wallpaper, global one or not. See **No wallpaper for one context** below. |
| Material surfaces | Menus, dialogs, dropdowns, the date picker, cards and the snackbar take the theme's own surfaces instead of Material's grey. Tooltips stay deliberately contrasting. |

### Icons

| Change | What it does |
| --- | --- |
| Planner icon | The built-in `next_week` glyph for Planner in the left navigation. |
| Schedule icons | `calendar_clock` for Schema in the left navigation and `pending_actions` on its right-panel button. |
| Dashboard icon | `avg_pace` for plugin entries in the left menu; it reaches every plugin row, not only Dashboard. |
| Play button icon | The play button keeps the app's own Material glyph, with the [Lucide Icons plugin](https://github.com/roosmsg/super-productivity-lucide-icons) installed or without it. Material Symbols carries a `FILL` axis and the app asks for the filled cut of play and pause; Lucide is stroke-only, so a solid mark there meant a second shape laid under the outline and kept registered by hand. Two declarations undo the plugin for this one element; every other icon is still drawn in Lucide. |
| Play glyph size | The play and pause glyphs are drawn a step above the size the app draws them, and the same size in the vertical rail and the top bar alike (`--play-glyph-scale`, `1` for the app's own size). |
| Play glyph colour | `paper-purple.css` and `shades-of-purple.css`. The filled play and pause glyphs are drawn white in both modes (`--play-icon-ink`), instead of taking the contrast colour the app computes from the project or tag colour. `shades-of-purple.css` hands that back on the disabled button; `paper-purple.css` keeps white throughout. |

### Type and scale

| Change | What it does |
| --- | --- |
| Typography | Inter throughout except the view title, which keeps the app's own stack; JetBrains Mono for code. Includes an override for Material's components, which compile their own font family and never read the variable. |
| Text rendering | Windows subpixel rendering is restored, which Material and the app switch off. Bold type caps at SemiBold and inline emphasis at Medium. |
| Content scale | Task lists, empty states and the finish-day action keep their `1.1` scale while the desktop Settings page zooms out to `0.9`. |
| Compact menus | The task context menu comes to 40px rows with a 12.5px label, and its tag, project and estimate submenus to 32px rows. |
| Tab selection | A straight line marks the selected tab instead of a filled, rounded shape. `minimal-tokyo.css` also moves the Settings indicator down onto the header rule and, in dark mode, keeps the selected label at the resting text colour. |
| Plugin manager | Rebalanced plugin cards: a 26px icon, a 20.5px name, and metadata in muted ink at 15.5px. |
| Scrollbars | No scrollbar in the task detail panel, on the summary page, in the main task views or in the left menu — all still scroll, only the bar is gone. |

## Wallpapers

Wallpapers are set through the app's own wallpaper dialog. Ones that suit these palettes:

- `minimal-tokyo.css`, dark mode — [a night street in Tokyo](https://images.unsplash.com/photo-1493515322954-4fa727e97985?ixid=M3w3NzgxMTF8MHwxfHNlYXJjaHwxN3x8bmlnaHR8ZW58MHwwfHx8MTc4Nzc3NDU5MHww&ixlib=rb-4.1.0&w=2560&q=85&auto=format): neon on wet asphalt in the same blues the palette is built from.
- The purple pair, dark mode — [a night sky over a mountain lake](https://images.unsplash.com/photo-1419242902214-272b3f66ee7a?ixid=M3w3NzgxMTF8MHwxfHNlYXJjaHw2fHxuaWdodHxlbnwwfDB8fHwxNzg3Nzc0NTkwfDA&ixlib=rb-4.1.0&w=2560&q=85&auto=format) or [a ship wreck at night](https://images.unsplash.com/photo-1513436539083-9d2127e742f1?ixid=M3w3NzgxMTF8MHwxfHNlYXJjaHwxNXx8bmlnaHR8ZW58MHwwfHx8MTc4Nzc3NDU5MHww&ixlib=rb-4.1.0&w=2560&q=85&auto=format): deep blues and violets the veil settles into.

### No wallpaper for one context

Super Productivity draws the global wallpaper on every project and tag that has no picture of its own, and there is no setting that says "none" for a single one. To keep the wallpaper on the Planner or Schedule but leave Inbox or My Day on the flat page colour, give that context a picture that is not a picture: `https://` or `null`, in project or tag → theme → background image, in the slot for the mode you use (there is one for light and one for dark).

The theme then treats the context as having no wallpaper at all — the image, the veil over it and the darkening floor beneath it are hidden, and every rule that keys on the app's `hasBgImage` class is guarded with the same test, so the view is styled exactly as it would be without a picture.

Three limits:

- A real address that merely begins with `https://` is not caught: the match is on the serialised URL together with its closing quote.
- The theme cannot put one context's picture on another page. Which image a page shows is decided by the app per route, so set that file as the global wallpaper instead.
- It cannot read which image is the global one, which is why a placeholder is needed rather than a rule like "hide the global wallpaper on tag pages".
