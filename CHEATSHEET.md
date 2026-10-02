# Cheatsheet — Ghostty

Only Ghostty's own defaults (nothing here is overridden by `config`, except the lines `config`
itself changes — `copy-on-select`, the colours, the font — which are visuals, not keys). Full list:
`ghostty +list-keybinds --default`. `Cmd` = `super` in Ghostty's own vocabulary.

⚠️ **Option+Left/Right vs tmux**: Ghostty claims plain `Option+Left`/`Option+Right` for word-jump
(`alt+arrow_left`/`alt+arrow_right`), which likely breaks `tmux-config`'s `M-Left`/`M-Right`
pane-navigation (expects a different escape sequence). Use **`Option+h/j/k/l`** instead — same
tmux binding, different (unclaimed) keys, works the same in Kitty/WezTerm/Ghostty alike.

## Window, tab, split

| Key | Does |
|---|---|
| `Cmd+N` | New window |
| `Cmd+T` | New tab |
| `Cmd+W` | Close the current split/pane |
| `Cmd+Shift+W` | Close the window |
| `Cmd+Opt+W` | Close the tab |
| `Cmd+Opt+Shift+W` | Close all windows |
| `Cmd+1`…`Cmd+8` | Go to tab 1–8 |
| `Cmd+9` | Go to the last tab |
| `Cmd+Shift+[` / `Cmd+Shift+]` | Previous / next tab |
| `Ctrl+Tab` / `Ctrl+Shift+Tab` | Next / previous tab |
| `Cmd+D` | Split right |
| `Cmd+Shift+D` | Split down |
| `Cmd+[` / `Cmd+]` | Go to previous / next split |
| `Cmd+Opt+Arrow` | Go to the split in that direction |
| `Cmd+Ctrl+Arrow` | Resize the split in that direction (step 10) |
| `Cmd+Ctrl+=` | Equalize all split sizes |
| `Cmd+Shift+Enter` | Toggle zoom on the current split |
| `Cmd+Enter` | Toggle fullscreen |

## Clipboard & selection

| Key | Does |
|---|---|
| `Cmd+C` / `Cmd+V` | Copy / paste |
| `Cmd+Shift+V` | Paste from the selection clipboard |
| `Shift+Arrow` | Extend the selection |
| `Shift+Home` / `Shift+End` | Extend selection to line start / end |
| `Cmd+A` | Select all |
| Mouse selection | **Does NOT auto-copy** — `copy-on-select` is off in `config` (Ghostty's own default is on) |

## Search

| Key | Does |
|---|---|
| `Cmd+F` | Start scrollback search |
| `Cmd+Shift+F` or `Esc` | End search |
| `Cmd+G` / `Cmd+Shift+G` | Next / previous match |
| `Cmd+E` | Search for the current selection |

## Scroll & prompt

| Key | Does |
|---|---|
| `Cmd+Home` / `Cmd+End` | Scroll to top / bottom |
| `Cmd+Page Up` / `Cmd+Page Down` | Scroll one page |
| `Cmd+Up` / `Cmd+Down` | Jump to previous / next shell prompt |
| `Cmd+J` | Scroll to the current selection |

## Editing in the shell (readline-style, not Ghostty-specific)

| Key | Does |
|---|---|
| `Option+Left` / `Option+Right` | Move back / forward one word (⚠️ see tmux warning above) |
| `Cmd+Left` / `Cmd+Right` | Jump to line start / end (sends `Ctrl+A` / `Ctrl+E`) |
| `Cmd+Backspace` | Delete to line start (sends `Ctrl+U`) |

## Font & config

| Key | Does |
|---|---|
| `Cmd+=` / `Cmd+-` | Increase / decrease font size |
| `Cmd+0` | Reset font size |
| `Cmd+,` | Open `config` in the default editor |
| `Cmd+Shift+,` | Reload config (also happens automatically on save) |

## Misc

| Key | Does |
|---|---|
| `Cmd+K` | Clear screen + scrollback |
| `Cmd+Z` / `Cmd+Shift+Z` | Undo / redo (Ghostty's own text-editing undo, not shell history) |
| `Cmd+Shift+P` | Command palette |
| `Cmd+Opt+I` | Toggle the inspector (Ghostty's own devtools) |
| `Cmd+Q` | Quit Ghostty |

## Not covered here

- `ghostty +list-fonts`, `+list-themes`, `+list-colors`, `+list-actions` — other CLI introspection
  actions, see `ghostty +help`.
- No light theme / no theme-switch key yet — see README's "Not carried over" section.
