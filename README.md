# Herdr configuration

Personal Herdr GUI customizations for transferring between machines.

## Included

- `layouts/andys-layout.json` — personal layout based on Herdr's `main` layout.
  It uses the custom tabs and Files mods below and omits the built-in Changes
  pane.
- `mods/pane-id/` — cloned pane header with the short terminal ID shown directly
  after the pane's working directory. Icons reference Herdr's originals.
  The header JavaScript must remain local: Herdr's module loader rejects imports
  outside the mod directory (including symlinks), and the built-in header has no
  extension slot for the ID.
- `mods/files-viewer/` — cloned Files panel. Markdown opens in `leaf`; other
  files open in `bat`. For extensionless files, the panel checks the first
  16 KiB for C++ syntax and header conventions. If it finds a match, it asks
  `bat` for C++ highlighting; otherwise `bat` uses its normal detection.
  Right-click a file to use Herdr's read-only preview instead. The `leaf`
  and `bat` tabs close when their viewers exit and show the full file path
  followed by the short terminal ID, without a separate working directory or
  icon. `bat` highlights in Solarized Dark by default (override with
  `BAT_THEME`); `ov` handles line numbers and wraps
  long lines when the pane resizes. Press `r` to reread and re-highlight in
  the same tab, `?` for help, or `q` to close. Backward search uses `Alt+/`.
  Expanded subfolders are remembered per working directory and machine,
  including across Herdr restarts.
- `mods/tabs-files/` — cloned tab bar. It removes the Changes button and adds
  a Lazygit button with a Git-style icon. Lazygit opens in the focused
  directory, focuses an existing Lazygit terminal for that directory, and
  closes its tab when Lazygit exits.
- `themes/solarized-dark.json` — Solarized Dark terminal and GUI theme.
- `themes/solarized-light.json` — Solarized Light terminal and GUI theme.

## Install

Copy the repository contents into the Herdr app home, preserving the
directory structure (normally `~/.config/herdr-app`):

```sh
cp -R layouts mods themes ~/.config/herdr-app/
```

Then select `andys-layout` in Herdr. The `leaf`, `bat`, `ov`, and `lazygit`
commands must be available on each machine where they are used.

Machine-specific state such as `settings.json`, `shared.json`, `view.json`,
window state, keys, and layout state is intentionally not included.

### Yazi shortcuts (optional)

The `herdr-yazi` plugin targets the older Herdr TUI. Herdr.app can launch Yazi
from the focused pane's working directory without a plugin. With `yazi`
installed on the machine running the terminal, merge these entries into
`global` in `~/.config/herdr-app/keys.json`:

```json
{
  "cmd-y": { "command": "terminal.open", "args": { "argv": ["yazi"], "place": "right", "name": "Yazi" } },
  "cmd-shift-y": { "command": "terminal.open", "args": { "argv": ["yazi"], "place": "tab", "name": "Yazi" } }
}
```
