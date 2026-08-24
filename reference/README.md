# Reference

Upstream artefacts, kept here to write themes against. None of them is a theme
and none is meant to be installed. Three are extracted from the packaged app
(`resources/app.asar`, Super Productivity 18.16.0) and belong to that project
under its own licence; `index2.html` is a snapshot of the app running on this
machine.

| File | What it is | Why it is here |
| --- | --- | --- |
| `dark-base.css` | The app's own `dark-base` theme | The shortest complete example of the variable contract a theme is expected to fill: surface ladder, ink, separators, and the component variables that follow from them. |
| `index.html` | The built page the app loads | Carries the inlined critical CSS, which is where the app declares its design tokens — spacing scale, radii, z-index ladder, transition timings, task metrics, and the palette ladders Material reads. Useful for looking up a variable name without unpacking the bundle again. |
| `index2.html` | A devtools snapshot of the running DOM, anonymised | Shows the rendered markup: live class names, the injected theme CSS, and the palette the app resolves at runtime. |
| `core-styles.css` | The app's global stylesheet, `styles-HS3AVNV3.css` | Where the variable contract is actually written: `--task-c-bg: var(--surface-2)`, `--task-c-selected-bg: var(--selected-task-bg-color)`, the spacing and radius scales, and the Material token defaults. Minified, but greppable — and it settles questions that guessing from the DOM cannot. |

`index2.html` is the third file: a snapshot of the running DOM, taken from the
devtools rather than from the bundle. It is the only one of the three that
shows the app as it actually renders — the resolved palette written onto the
`<html>` element as an inline `style` attribute, the theme's own CSS as the app
injects it, and every component with its live classes. That makes it the file
to reach for when a selector needs checking. It also carried whatever was on
screen when it was taken, so the project names, the tag on the visible task and
that task's title were replaced with placeholders (`Project A`…`Project E`,
`Example task`). Structure, class names and styling are untouched. Anything
added later needs the same pass before it is committed.
