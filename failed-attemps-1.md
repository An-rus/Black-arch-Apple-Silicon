# ❌ GUI Setup Attempts

> Attempting to set up Hyprland/bspwm on OrbStack via X11 forwarding. Deprioritized in favor of terminal workflow.

---

## Goal
- WM: Hyprland (tiling, Wayland)
- Terminal: Kitty with transparency
- Theme: Space/quantum aesthetic
- Wallpaper: Animated black hole

---

## ❌ Attempt 1 — startx in OrbStack

```bash
echo "exec bspwm" > ~/.xinitrc
startx
```

**Error:** `Only console users are allowed to run the X server`

**Root cause:** OrbStack containers don't have `/dev/tty` — Xorg requires a virtual console to start.

---

## ❌ Attempt 2 — Alacritty via SSH X11 Forwarding

Installed XQuartz 2.8.5, enabled X11Forwarding in sshd_config, connected with `ssh -X`.

**Error:** `neither WAYLAND_DISPLAY nor DISPLAY is set`

**Root cause:** Alacritty requires GPU/Wayland. It doesn't support X11 forwarding.

---

## ❌ Attempt 3 — xterm via X11 Forwarding

```bash
export DISPLAY=localhost:10.0
xterm
```

**Error:** `Can't open display: localhost:10.0`

**Root cause:** XQuartz 2.8.5 bug on recent macOS — `xhost` binary missing from `/opt/X11/bin/`.

---

## Why Deprioritized

- All pentesting tools work perfectly from terminal
- GUI is aesthetic only, no security capability added
- Proper solution requires VMware Fusion or Homebrew XQuartz fix

---

## Future Plan

- **Option A:** VMware Fusion Pro (free) — full VM, Hyprland native
- **Option B:** `brew install --cask xquartz` — fixes xhost issue
- **Option C:** VNC server inside OrbStack
