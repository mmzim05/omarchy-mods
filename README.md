# omarchy-mods

Small add-ons for [Omarchy](https://omarchy.org) that add install scripts and
rows to the Omarchy menu.

| Mod | Adds |
|-----|------|
| `appimage` | **Install > AppImage**: pick AppImages in `~/Downloads`, install or update them in `~/Applications` with a launcher entry and icon. **Remove > AppImage**: remove them again. |
| `flatpak` | **Install > Flatpak**: fuzzy-search Flathub and install apps (sets up flatpak and the Flathub remote on first use). |
| `davinci-resolve` | **Install > Editor > DaVinci Resolve**: build and install DaVinci Resolve Studio from the `DaVinci_Resolve_Studio_<version>_Linux.zip` in `~/Downloads`, using the AUR `davinci-resolve-studio` package patched to that version. |

## Install

```bash
git clone https://github.com/mmzim05/omarchy-mods ~/.local/share/omarchy-mods
~/.local/share/omarchy-mods/mods install appimage flatpak davinci-resolve
```

## Usage

```
mods list               Show available mods and which are installed
mods install <mod...>   Install mods, or reinstall them to pick up changes
mods update             Pull this repo, then reinstall every installed mod
mods remove <mod...>    Remove mods' scripts and menu rows
```

Each mod is a folder with:

- `bin/`: scripts copied into `~/.local/bin`.
- `menu.jsonc`: Omarchy menu rows, written into
  `~/.config/omarchy/extensions/omarchy-menu.jsonc` between
  `// omarchy-mods:<mod> start` and `end` markers. Everything outside the
  markers is left alone.

Installed mods are recorded in `~/.local/state/omarchy-mods/installed`.
