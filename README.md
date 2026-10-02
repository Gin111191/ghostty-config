# ghostty-config

Ghostty on macOS, made to look like [kitty-config](https://github.com/Gin111191/kitty-config) and
[wezterm-config](https://github.com/Gin111191/wezterm-config): Dusk-Navy, JetBrainsMono Nerd Font
Mono 13, 0.94 opacity with the desktop blurred behind, `copy-on-select` turned off (Ghostty's own
default silently copies on every mouse selection, unlike kitty/WezTerm).

```sh
git clone https://github.com/Gin111191/ghostty-config ~/.config/ghostty
```

Needs JetBrainsMono Nerd Font installed (same **Mono** variant kitty uses). Ghostty reloads the
file the moment it is saved (or `Cmd+Shift+,`).

Ghostty on macOS actually reads config from here (`$XDG_CONFIG_HOME/ghostty/config`, confirmed with
`ghostty +show-config`) even though it also keeps an unused, empty file at `~/Library/Application
Support/com.mitchellh.ghostty/config.ghostty`. If `XDG_CONFIG_HOME` is unset on a machine, Ghostty
falls back to `~/.config/ghostty/config` anyway, so the clone path above should still work.

| File | What it holds |
|---|---|
| `config` | Everything; each line that is not a default says why |

## Not carried over from kitty/WezTerm

- **Light theme + a switch key** — kitty has `dark-theme.conf`/`light-theme.conf` swapped with
  `CMD+OPT+↓`/`↑`; WezTerm follows the OS automatically. Ghostty here only ships the one static
  Dusk-Navy palette — no light variant, no keybind. (Note if adding one later: Ghostty's own
  default binds `super+alt+arrow_*` to `goto_split`, so reusing kitty's exact keys would collide
  with that — pick different keys or unbind the split action first.)
- **Following the system's dark/light switch** — same gap as kitty, for the same reason.
- **The background gradient / status strip** — WezTerm-only features.

## Images in Neovim

[nvim-config](https://github.com/Gin111191/nvim-config#images--snacksimage) draws images through
Ghostty the same way it does through kitty — both speak the Kitty graphics protocol. `config` here
clears `TMUX`/`TMUX_PANE`/`TERM_PROGRAM`/`TERM_PROGRAM_VERSION` from Ghostty's shells, same reason
kitty-config does: a Ghostty window started from inside another terminal's tmux pane would
otherwise pass those along and make Neovim wrap every image for a tmux that is not there.

Under tmux specifically, nvim-config's `image.lua` detects the attached client by name
(`tmux display-message -p '#{client_termname}'`) and only recognised `"kitty"` until this was
added — a plain Ghostty+tmux session drew nothing even though Ghostty can render. Fixed in
nvim-config to also match `"ghostty"`.
