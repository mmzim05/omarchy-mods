# omarchy-mods

Small add-ons for [Omarchy](https://omarchy.org): install scripts and Omarchy
menu rows, plus a laptop lid tweak.

| Mod | Adds |
|-----|------|
| `appimage` | **Install > AppImage**: pick AppImages in `~/Downloads`, install or update them in `~/Applications` with a launcher entry and icon. **Remove > AppImage**: remove them again. |
| `flatpak` | **Install > Flatpak**: fuzzy-search Flathub and install apps (sets up flatpak and the Flathub remote on first use). |
| `nerd-font` | **Install > Style > Font > Any Nerd Font**: fuzzy-search every font on [nerdfonts.com](https://www.nerdfonts.com/font-downloads), and install it into `~/.local/share/fonts/NerdFonts` for use in any app. The system font is not changed. |
| `davinci-resolve` | **Install > Editor > DaVinci Resolve**: build and install DaVinci Resolve Studio from the `DaVinci_Resolve_Studio_<version>_Linux.zip` in `~/Downloads`, using the AUR `davinci-resolve-studio` package patched to that version. |
| `restart-to-windows` | **System > Restart to Windows**, above Reboot and Shutdown: reboots once into Windows by setting the firmware's `BootNext` to Windows Boot Manager, for dual-boot machines where the boot menu can't be seen. Run `omarchy-restart-to-windows --setup` once after installing: it asks for your sudo password and adds `/etc/sudoers.d/omarchy-restart-to-windows`, which allows only `efibootmgr --bootnext <Windows entry>` without a password. The row is hidden until that rule is in place. `mods remove` doesn't delete the rule: run `sudo rm /etc/sudoers.d/omarchy-restart-to-windows`. |
| `stay-awake-lid` | While the bar's **Stay Awake** toggle is on, closing the laptop lid no longer suspends, so processes keep running. Each lid close plays a warning tone twice, even when the speaker is muted. |

## Install

```bash
git clone https://github.com/mmzim05/omarchy-mods ~/.local/share/omarchy-mods
~/.local/share/omarchy-mods/mods install appimage flatpak nerd-font davinci-resolve
```

## Usage

```
mods list               Show available mods and which are installed
mods install <mod...>   Install mods, or reinstall them to pick up changes
mods update             Pull this repo, then reinstall every installed mod
mods remove <mod...>    Remove mods' scripts, units and menu rows
```

Each mod is a folder with:

- `bin/`: scripts copied into `~/.local/bin`.
- `systemd/`: user units copied into `~/.config/systemd/user`. Units with an
  `[Install]` section are enabled and started. Running units aren't
  restarted; they pick up changes the next time they start.
- `menu.jsonc`: Omarchy menu rows, written into
  `~/.config/omarchy/extensions/omarchy-menu.jsonc` between
  `// omarchy-mods:<mod> start` and `end` markers. Everything outside the
  markers is left alone.

Installed mods are recorded in `~/.local/state/omarchy-mods/installed`.
