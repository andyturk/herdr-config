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
- `mods/files-leaf/` — cloned Files panel. Clicking `.md` and `.markdown`
  files opens them in `leaf`; other files keep Herdr's normal preview.
  Leaf tabs close automatically when `leaf` exits.
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

Then select `andys-layout` in Herdr. The `leaf` and `lazygit` commands must be
available on each machine where they are used.

Machine-specific state such as `settings.json`, `shared.json`, `view.json`,
window state, keys, and layout state is intentionally not included.
