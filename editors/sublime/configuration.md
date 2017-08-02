---
layout: section
order: 3
title: Configuration
---

## Line Endings (Windows Users)

Windows users should ensure the `Line Endings` setting is set to `Unix`. Go to *View Menu / Line Endings* and select *Unix*.

## Mouse Clicks

ENSIME Sublime customizes mouse bindings. It makes `Ctrl+Click`/`Cmd+Click` invoke `Go to Definition` and `Shift+Click` stand for `Inspect Type at Point`.

These bindings can be altered in the the config: *Preferences Menu / Package Settings / Ensime / Mousemap - Default*.

## Key Bindings

- `Ctrl+Alt+e` invokes `Show errors and warnings` which displays the error and warning messages below the highlighted areas.
- `Ctrl+Alt+c` invokes `Classpath search`
- `Ctrl+Alt+g` invokes `Go to definition`
- `Ctrl+Alt+f` invokes `Find usages`
- `Ctrl+Alt+d` invokes `Show implementations`
- `Ctrl+Alt+i` invokes `Add import`
- `Ctrl+Alt+o` invokes `Organise imports`
- `Ctrl+Space` on Windows/OS X and `Alt+/` on GNU/Linux invokes code completion by default.

Other keybindings can be enabled in the config: *Preferences Menu / Package Settings / Ensime / Keymap - Default*.
