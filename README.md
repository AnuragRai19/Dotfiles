# Hyprland Setup Guide

A comprehensive guide for setting up Hyprland on Arch Linux.

---

## Phase 1: Installation

### 1. Install Core Packages

After a fresh install of Arch, install the following essentials:

**Base:**

- `kitty` - Terminal emulator
- `rofi` - Application launcher
- `hyprland` - Window manager

**File Management:**

- `thunar` - File manager
- `thunar-archive-plugin` - Archive support for Thunar
- `tumbler` - Thumbnail generator
- `gvfs` - Virtual filesystem

**Archivers:**

- `file-roller` - Archive manager
- `p7zip` - 7z compression
- `unrar` - RAR extraction
- `unzip` - ZIP extraction

**Tools:**

- Your preferred text editor
- An AUR helper (like `yay`)

### 2. Setup Display Manager

Install SDDM and enable it to start on boot:

```bash
sudo systemctl enable sddm
```

---

## Phase 2: Setup and Configuration

### 1. Configure Hyprland

After reboot, start setting up Hyprland using the Hyprland configuration file.

### 2. Install XDG Desktop Portal

```bash
yay -S xdg-desktop-portal-hyprland-git
```

### 3. Install Authentication Agent (Polkit GNOME)

Install the Polkit GNOME agent:

```bash
sudo pacman -S polkit-gnome
```

Locate the agent binary:

```bash
ls /usr/lib/polkit-gnome/
```

The binary should be at: `/usr/lib/polkit-gnome/polkit-gnome-authentication-agent-1`

Add this line to your Hyprland config to autostart the agent:

```bash
exec-once = /usr/lib/polkit-gnome/polkit-gnome-authentication-agent-1
```

Verify the installation:

```bash
pkexec env DISPLAY=$DISPLAY XAUTHORITY=$XAUTHORITY xterm
```

### 4. Install Hyprland Utilities

Install and configure the following:

- `hyprpaper` - Wallpaper manager
- `hyprlock` - Screen locker
- `hypridle` - Idle management

### 5. Install Additional Tools

```bash
sudo pacman -S cliphist hyprshot hyprpicker wf-recorder celluloid
```

- `cliphist` - Clipboard manager
- `hyprshot` - Screenshot tool
- `hyprpicker` - Color picker
- `wf-recorder` - Screen recorder
- `celluloid` - Video player

### 6. Install Image Viewer

```bash
sudo pacman -S gthumb
```

---

## Phase 3: Theming

### 1. Install Theme Manager

```bash
sudo pacman -S nwg-look
```

### 2. Choose and Install Themes

1. Browse themes at [gnome-look.org](https://www.gnome-look.org)
2. Download your preferred theme
3. Place themes in `~/.themes/` folder
4. Place icons in `~/.icons/` folder

### 3. Configure Fonts and Terminal

1. Place fonts in `~/.fonts/` or `~/.local/share/fonts/`
2. Run `fc-cache -fv` to refresh font cache
3. Configure your terminal (kitty) appearance and fonts

---
