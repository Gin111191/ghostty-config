# ghostty-config

Ghostty on macOS, made to look like [kitty-config](https://github.com/Gin111191/kitty-config) and
[wezterm-config](https://github.com/Gin111191/wezterm-config): Dusk-Navy, JetBrainsMono Nerd Font
Mono 13, 0.94 opacity with the desktop blurred behind, `copy-on-select` turned off (Ghostty's own
default silently copies on every mouse selection, unlike kitty/WezTerm).

```sh
git clone https://github.com/Gin111191/ghostty-config ~/.config/ghostty
ln -sf ~/.config/ghostty/config \
  ~/Library/Application\ Support/com.mitchellh.ghostty/config.ghostty
```

Needs JetBrainsMono Nerd Font installed (same **Mono** variant kitty uses). Ghostty reloads the
file the moment it is saved (or `Cmd+Shift+,`).

**The second line above is not optional, even though Ghostty's docs make `$XDG_CONFIG_HOME/ghostty/
config` sound like the real path.** Running the `ghostty` *CLI* binary from a shell does read that
XDG path — confirmed with `ghostty +show-config` — because the shell has already exported
`XDG_CONFIG_HOME`. But the *GUI* app, opened from the Dock/Spotlight/Finder, is started by `launchd`
with its own environment, which does **not** include anything your `.zshenv` exports — macOS GUI
apps never inherit a shell's environment this way. So `Ghostty.app` itself always falls back to its
native macOS path, `~/Library/Application Support/com.mitchellh.ghostty/config.ghostty`, no matter
what `$XDG_CONFIG_HOME` is set to in any shell. Symptom if the symlink step above is skipped: the
file at `~/.config/ghostty/config` is correct and `ghostty +show-config` from a terminal shows all
the right values, but the actual window never changes — because the running app is reading its
own, separate, empty file instead. The symlink makes both paths resolve to the one real file.

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
