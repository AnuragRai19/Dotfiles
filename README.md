# Niri Setup Guide

This repository contains my personal configurations (**dotfiles**) for a keyboard-driven, minimal, and high-performance Wayland environment. Built on **CachyOS** (Arch-based), this setup focuses on the **Niri** scrolling compositor and the **Noctalia** shell.

---

### Key Components:
* **Compositor:** [Niri](https://github.com/YaLTeR/niri) (A scrollable-tiling Wayland compositor).
* **OS:** [CachyOS](https://cachyos.org/) (Optimized Arch Linux using x86_64-v3 binaries).
* **Shell/Bar:** **Noctalia** (Built on [Quickshell](https://github.com/outfoxxed/quickshell)).
* **Terminal:** [Kitty](https://sw.kovidgoyal.net/kitty/) with [Zsh](https://www.zsh.org/) and [Starship](https://starship.rs/).
* **App Launcher:** [Fuzzel](https://codeberg.org/dnkl/fuzzel).
* **Theme Management:** `nwg-look` (GTK3/4).

---

## Phase 1: Base System & Compositor Architecture

My environment begins with a minimal **CachyOS** installation. I opted for a TTY-only base to ensure zero bloat and to have full control over the display stack.

### The Display Stack
Since I am targeting a modern, secure, and performant workflow, I migrated entirely to **Wayland**. The core of this phase involves the installation of the Niri compositor and its X11 compatibility layer for legacy applications.

```bash
# Core Installation
sudo pacman -S niri xwayland-satellite-bin
```

### Phase 2. Compositor Configuration (`config.kdl`)

Niri uses the **KDL** configuration format, which is highly readable and structured. I have organized my configuration into three simplified sections to ensure a maintainable and efficient system:

* **Layout (Horizontal Scrolling):** Unlike traditional tiling managers that shrink windows to fit the screen, I use a **Horizontal Scrolling** logic. Windows maintain a usable width and "scroll" off-screen as new ones open, creating an infinite horizontal workspace that prevents visual clutter.
* **Input Tuning:** I have fine-tuned the **keyboard repeat rates** and mouse sensitivity. This ensures a "snappy" and responsive feel, which is critical for maintaining flow during long programming sessions.
* **Keybindings:** The system is entirely keyboard-driven to minimize hand movement. I use the `Super` (Windows) key for all core system actions:
    * `Super + Enter`: Open Terminal (Kitty)
    * `Super + Q`: Close Window
    * `Super + H/L`: Scroll focus between windows
* These are just some examples of what you can do refer to my config.kdl for more understanding or use niri documentation.

## Phase 3: Interface & Theming (Noctalia + Matugen)

Once the compositor was stable, I implemented a unified UI using **Noctalia**, a modular shell built on **Quickshell**. My setup leverages Noctalia's native integration with **Matugen** to create a seamless "Material You" experience across the entire system.

* **Dynamic Material You Theming:** I use **Matugen** as the core color engine. By extracting color palettes directly from my wallpaper, Noctalia generates a Material Design scheme that updates in real-time whenever the background changes.
* **Built-in Template System:** I have configured Noctalia’s internal template engine to automatically inject these dynamic colors into critical applications, ensuring a zero-maintenance cohesive look. This includes:
    * **GTK 3/4 & Qt6ct:** Consistent theming for both GNOME and KDE-based applications.
    * **Terminals:** Automatic color injection for **Kitty**, ensuring the dev environment matches the desktop aesthetic.
    * **System UI:** Real-time synchronization of the **Noctalia bar**, **Fuzzel** launcher, and notification system.
* **Status Orchestration:** Beyond aesthetics, the Noctalia shell provides a high-performance status bar, workspace indicators, and an integrated control center for system management.

## Phase 3: Services & Automation

In this phase, I configured the "plumbing" of the environment, automating background services and security protocols within Niri's config.kdl to ensure a seamless, production-ready workflow.

### 1. Startup Orchestration
I use Niri's `spawn-at-startup` and `spawn-sh-at-startup` directives to initialize my environment automatically upon login. This ensures that critical UI and utility components are always ready: 
* **Noctalia Shell:** Initialized via `qs -c noctalia-shell` to provide the status bar and desktop interface. 
* **Security & Authentication:** Automated the `polkit-gnome` authentication agent to handle graphical elevation requests. 
* **Clipboard Management:** Integrated `wl-paste` with `cliphist` to maintain a persistent, searchable history for both text and images.
  
### 2. Power Management & Idle Handling
To ensure system longevity and security, I implemented a complex **swayidle** configuration. This script manages multiple states based on inactivity: 
* **Locking:** Automatically triggers the Noctalia lock screen after 10 minutes of inactivity. 
* **Power Saving:** Powers off monitors after 10.5 minutes and triggers a full system `suspend` after 30 minutes. 
* **Sleep Hooks:** Ensures the screen is locked immediately before the system enters a sleep state. 

### 4. Integrated Keybindings & Workflow
My `binds` section is customized for high-speed navigation, utilizing the **Super (Mod)** key for a streamlined experience: 
* **Quick Launch:** Direct bindings for **Kitty** (Mod+T), **Brave** (Mod+B), **VS Code** (Mod+C), and **Nautilus** (Mod+E). 
* **Utility Tools:** Integrated **Fuzzel** for application launching (Mod+Space) and a custom clipboard history picker (Mod+V) using `fuzzel --dmenu`. 
* **Window Management:** Leverages Niri's unique "column" logic with `consume-or-expel` (Mod+Bracket) and `switch-preset-column-width` (Mod+R) for dynamic layout adjustments. 
