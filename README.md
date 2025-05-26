# Ptyxis: Your Container-Oriented Terminal for GNOME

Ptyxis is a terminal emulator for the GNOME desktop, engineered for first-class integration with local containerized environments such as Podman, Toolbox, and Distrobox. It aims to simplify and enhance your interaction with these tools, making them a natural extension of the terminal workflow.

![Ptyxis Screenshot - Tab Overview](https://gitlab.gnome.org/chergert/ptyxis/-/raw/main/data/screenshots/tab-overview.png)
*Fig 1: Tab overview for managing multiple terminal sessions.*

## Installation

**Recommended: Flatpak (Nightly)**
Ptyxis is designed with Flatpak as its primary distribution method. You can install the development version from the GNOME Nightly repository:

```bash
flatpak install --user --from https://nightly.gnome.org/repo/appstream/org.gnome.Ptyxis.Devel.flatpakref
```

**Building from Source**
Ptyxis uses the Meson build system.
1.  Ensure you have all necessary dependencies: C compiler, Meson (>=1.0.0), Ninja, GLib (>=2.80), GTK4 (>=4.14), Adwaita (>=1.6), JSON-GLib (>=1.6), VTE (>=0.79), and libportal-gtk4 (on Linux).
2.  Clone the repository: `git clone https://gitlab.gnome.org/chergert/ptyxis.git`
3.  Navigate into the directory: `cd ptyxis`
4.  Configure the build: `meson setup _build` (add options like `--prefix=/usr/local` if needed)
5.  Compile: `meson compile -C _build`
6.  Install: `sudo meson install -C _build`

[GNOME Builder](https://apps.gnome.org/Builder/) is also recommended. You can open the cloned `ptyxis/` directory directly in Builder (`flatpak run org.gnome.Builder -p ptyxis/`) for an integrated build and development experience.

## Basic Usage & Command-Line Options

Launch Ptyxis by running `ptyxis` from your application launcher or another terminal.

**Common Command-Line Options:**

*   `--version`: Show the program version.
*   `--preferences`: Open the preferences window.
*   `--new-window`: Open a new window in an existing instance.
*   `--tab`: Open a new tab in the most-recently-used window.
*   `--tab-with-profile=PROFILE_UUID`: Open a new tab using the specified profile UUID.
*   `-x "COMMAND"`, `--execute "COMMAND"`: Execute a custom command string in a new window (implies standalone mode).
*   `-- PROGRAM [ARGUMENTS...]`: Execute `PROGRAM` with `ARGUMENTS` in a new window (implies standalone mode).
*   `-d DIR`, `--working-directory DIR`: Set the working directory for a new tab/window or custom command.
*   `--title=TITLE`: Set the initial title for a new tab/window.
*   `--maximize`: Maximize a newly created window.
*   `--fullscreen`: Fullscreen a newly created window.
*   `--import-palette=FILE`: Import a Ptyxis `.palette` file into your user configuration.
*   `-s`, `--standalone`: Start a new instance of Ptyxis, ignoring any already running.
*   `-h`, `--help`: Show a summary of options.

## Core Functionality & Design

Ptyxis provides robust terminal emulation capabilities via the VTE widget, enhanced with a GTK4/Adwaita user interface. Its architecture is two-part:

1.  **UI Application:** Manages windows, tabs, profiles, theming (palettes), keyboard shortcuts, and user preferences.
2.  **`ptyxis-agent`:** A distinct helper process running on the host (or sandboxed as a fallback). It handles operations requiring broader system access: PTY creation, direct interaction with container runtimes, and host-level process monitoring. The UI communicates with the agent via D-Bus.


## Container Integration: Technical Details

Ptyxis interacts directly with container management tools installed on the host system through its `ptyxis-agent`:

1.  **Discovery:** The agent queries the host for available containers (e.g., `podman ps --all --format=json`) and monitors system files (like `containers.json` or Podman's `db.sql`) for dynamic updates to the container list presented in the UI.
2.  **Spawning:** When launching a terminal in a container, the agent constructs and executes the appropriate CLI commands for the target runtime (e.g., `podman exec -it ...`, `toolbox enter ...`, `distrobox enter --no-tty ... --`). It manages PTY setup and I/O redirection.
3.  **Context Management:**
    *   The agent and VTE terminal properties (termprops like `vte.container.name`) identify the active container.
    *   Working directories and selected environment variables (e.g., host proxies if `use-proxy` is enabled in the profile) can be propagated into containers.
    *   Profiles can specify a default container and behavior for inheriting container context or CWD in new tabs.
    *   URI translation is supported for actions like "Open Link" from within containers.

![Container Selection Menu](https://gitlab.gnome.org/chergert/ptyxis/-/raw/main/data/screenshots/containers-menu.png)
*Fig 2: Containers are automatically discovered and displayed in the "New Tab" menu.*

## `ptyxis-agent` Functions

The `ptyxis-agent` is a critical component that:
*   Manages PTY creation and setup.
*   Spawns processes on the host and, more importantly, inside containers.
*   Interacts with container runtimes for discovery and command execution.
*   Retrieves host system information (default shell, OS name, proxy settings).
*   Monitors spawned processes, tracks foreground processes, and reports their status/exit codes to the UI.
*   Is designed for portability, especially on x86_64, using GLIBC symbol versioning to target older systems like GLIBC 2.17.
*   Exposes its functionalities via D-Bus for the UI to consume.

## Supported Container Technologies

Ptyxis offers direct support for seamless interaction with several local container technologies:
*   **Podman:** Full support.
*   **Toolbox:** Supported.
*   **Distrobox:** Supported.
*   **JHBuild:** Supported as a special environment; commands are prefixed with `jhbuild run`.
    *   For optimal JHBuild session persistence with Ptyxis, add the following to your `~/.bashrc` (or equivalent shell startup file):
        ```bash
        if [ -t 1 -a x$UNDER_JHBUILD != x ]; then
            printf "\033]777;container;push;%s;jhbuild\033\\" "JHBuild"
            function pop_container {
                printf "\033]777;container;pop;;\033\\"
            }
            trap pop_container EXIT
        fi
        ```
*   **Docker:** Direct, dedicated support for the Docker daemon is **not currently implemented**.

**Note on Container Security:** Ptyxis currently assumes that containers are not used for strict security isolation, as most general-purpose container runtimes may not provide sufficient hardening for all untrusted workloads.

## Key Features Overview

*   **Container Integration:** Automatic discovery, direct spawning, context preservation (container, CWD), visual indicators for containerized/sudo/remote processes.
*   **UI & UX:** Modern Adwaita/GTK4 interface, tabbed browsing with a **searchable tab overview**, pinned tabs, session restore.
*   **Profiles & Customization:** Named profiles for customizing default container, commands, appearance, various terminal behaviors, and **robust compatibility modes**.
*   **Theming:**
    *   Extensive built-in color palettes with automatic light/dark mode switching.
    *   User-installable custom `.palette` files (placed in `~/.local/share/ptyxis/palettes` or `~/.local/share/org.gnome.Ptyxis.Devel/palettes`).
    *   "Window Dressing" feature dynamically applies palette colors to the entire window theme.
    *   Optional terminal background transparency.
*   **Terminal Emulation (VTE):** Scrollback search, hyperlink handling, configurable key bindings, CJK ambiguous width character support, text blinking modes.
*   **Accessibility:** Designed with accessibility at its core, leveraging GTK4's accessibility stack enhancements contributed to VTE, making the terminal usable for everyone.
*   **High-Performance Rendering:** Utilizes VTE, which has received significant performance improvements including GPU-accelerated rendering (via Vulkan or OpenGL), ensuring a responsive and fluid user experience.
*   **Shortcuts:** Highly configurable keyboard shortcuts.
*   **`ptyxis-agent`:** Manages privileged operations and host system interactions, allowing for cleaner separation of concerns and facilitating Flatpak distribution.
*   **Systemd Scopes:** Terminal tabs run in separate systemd user scopes (if `systemd-run` is available and sufficiently new) for better resource isolation.
*   **Terminal Inspector:** A developer tool for debugging terminal-based applications, allowing users to peek at details like **OSC hyperlinks, mouse event coordinates**, and other diagnostic information.

![Preferences: Behavior Settings](https://gitlab.gnome.org/chergert/ptyxis/-/raw/main/data/screenshots/change-behavior.png)
*Fig 3: Many behaviors of the terminal may be tweaked to user preference.*

![Keyboard Shortcut Customization](https://gitlab.gnome.org/chergert/ptyxis/-/raw/main/data/screenshots/shortcut-editing.png)
*Fig 4: Many shortcuts may be remapped to user preference.*

![Palette Selector](https://gitlab.gnome.org/chergert/ptyxis/-/raw/main/data/screenshots/palette-selector.png)
*Fig 5: Built-in color palettes provide both dark and light mode variants.*

![Profile Editor](https://gitlab.gnome.org/chergert/ptyxis/-/raw/main/data/screenshots/edit-profile.png)
*Fig 6: Profiles allow for overriding a number of features such as default container.*

![Sudo Process Indication](https://gitlab.gnome.org/chergert/ptyxis/-/raw/main/data/screenshots/sudo-tracking.png)
*Fig 7: The terminal visually indicates when you're operating as root.*

![SSH Remote Process Indication](https://gitlab.gnome.org/chergert/ptyxis/-/raw/main/data/screenshots/ssh-tracking.png)
*Fig 8: Visual cue when connected to a remote system via SSH.*

## How It Works (Agent-UI Interaction & Fallbacks)

Ptyxis UI communicates with `ptyxis-agent` via D-Bus over a `socketpair()`. The agent is designed for portability to run on the host system. Even when the Ptyxis UI is run as a Flatpak, it requires permissions (like `org.freedesktop.Flatpak` for `flatpak-spawn --host`) that grant it significant access to the host system to enable its agent and container features. If host execution of the agent fails (e.g., due to incompatible GLIBC on systems like Alpine, or non-standard linker paths on NixOS), Ptyxis attempts to run `ptyxis-agent` within its own Flatpak sandbox as a fallback. This fallback may limit some host-interaction features but ensures basic functionality.

## Feature Requests and Design Changes

Ptyxis uses its GitLab issue tracker primarily for engineering defects. For new features or significant design changes:

1.  **Initiate Discussion:** Start by discussing your idea or proposal, preferably through the [GNOME Design Whiteboards project](https://gitlab.gnome.org/Teams/Design/whiteboards/) or by opening a discussion-focused issue on the Ptyxis GitLab.
2.  **Develop a Specification:** For larger features, a detailed specification is required. This should cover:
    *   How the feature should work and not work.
    *   Interaction with existing features.
    *   Any necessary migration strategies.
    *   UI mock-ups (if applicable).
    *   Testing strategy.
    *   Potential risks and security considerations.
    *   Ideally, an indication of who might implement it.

Once a design is well-defined, an issue can be filed on the Ptyxis tracker referencing the design discussion/specification.

## Known Issues & Troubleshooting

*   **Notifications Don't Work:** Ensure your shell (e.g., in `~/.bashrc` or `~/.zshrc`) sources `/etc/profile.d/vte.sh`. This file provides the necessary shell-side hooks for VTE's terminal property escape sequences, which Ptyxis uses for features like command completion notifications.
*   **GPU/Font Rendering Issues:** Problems with GPU rendering or font rendering are often rooted in the underlying GTK or VTE libraries. Consider reporting such issues to the respective GNOME/gtk or GNOME/vte projects.

## License

Ptyxis is licensed under the **GNU General Public License v3.0 or later**.
The source code includes a copy of the license in the `COPYING` file.
