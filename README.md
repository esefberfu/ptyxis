<p align="center">
  <img src="https://gitlab.gnome.org/chergert/ptyxis/-/raw/main/data/icons/ptyxis.svg" alt="Ptyxis Logo" width="150"/>
</p>

# Ptyxis: Your Container-Oriented Terminal for GNOME

<p align="center">
  <a href="https://gitlab.gnome.org/chergert/ptyxis/-/blob/main/COPYING">
    <img alt="License: GPL v3+" src="https://img.shields.io/badge/License-GPL%20v3%2B-blue.svg">
  </a>
  <a href="https://gitlab.gnome.org/chergert/ptyxis/-/pipelines">
    <img alt="GitLab Pipeline Status" src="https://gitlab.gnome.org/chergert/ptyxis/badges/main/pipeline.svg">
  </a>
  <a href="https://flathub.org/apps/app.devsuite.Ptyxis">
    <img alt="Distribution: Flatpak" src="https://img.shields.io/badge/Available%20on-Flatpak-4d9c9a.svg?logo=flatpak&logoColor=white">
  </a>
  <!--
  <a href="https://apps.gnome.org/app/app.devsuite.Ptyxis/">
    <img alt="GNOME App Page (Illustrative)" src="https://img.shields.io/badge/GNOME-App%20Page-brightgreen.svg">
  </a>
  -->
</p>

<p align="center">
  <strong>A modern terminal emulator built for the container era.</strong><br/>
  <em>Seamlessly navigate between your host system and local containers like Podman, Toolbox, and Distrobox with intelligent detection and a beautiful, responsive GNOME interface.</em>
</p>

<p align="center">
  <img src="https://gitlab.gnome.org/chergert/ptyxis/-/raw/main/data/screenshots/tab-overview.png" alt="Ptyxis Screenshot - Tab Overview" width="700"/>
</p>
*Fig 1: Ptyxis tab overview for managing multiple terminal sessions.*

---

<p align="center">
  <a href="#-what-makes-ptyxis-special">What is Ptyxis?</a>  • 
  <a href="#-key-features">Key Features</a>  • 
  <a href="#-screenshots">Screenshots</a>  • 
  <a href="#-installation">Installation</a>  • 
  <a href="#️-basic-usage--command-line-options">Usage</a>  • 
  <a href="#-container-integration">Container Integration</a>  • 
  <a href="#-contributing-feature-requests-and-design-changes">Contributing</a>  • 
  <a href="https://gitlab.gnome.org/chergert/ptyxis/-/issues">Report an Issue</a>
</p>

---

## ✨ What Makes Ptyxis Special?

Ptyxis (formerly "Prompt") isn't just another terminal emulator—it's engineered from the ground up for modern development workflows within the GNOME desktop, where local containers are first-class citizens. It simplifies and enhances your interaction with tools like Podman, Toolbox, and Distrobox, making them a natural extension of your terminal experience. Ptyxis is becoming the default terminal in Fedora Workstation and is under consideration for future Ubuntu releases, highlighting its robust design and performance.

### 🚀 Key Features

*   **🥇 First-Class Container Integration**: Automatic discovery, direct spawning, and context preservation (active container, CWD) for Podman, Toolbox, Distrobox, and JHBuild.
*   **📱 Modern GNOME Interface**: Built with GTK 4 and libadwaita for a native, responsive, and accessible user experience, adhering to GNOME HIG.
*   **🎨 Dynamic Theming & Customization**: Extensive built-in color palettes that automatically adapt to system light/dark modes. Supports user-installable custom `.palette` files and "Window Dressing" for full-window theming.
*   **⚡ Smart Process Tracking**: Visual indicators for `sudo` sessions, active SSH connections, and other foreground processes, enhancing situational awareness.
*   **📋 Advanced Tab Management**: Searchable tab overview with live previews and pinned tabs that persist their session context (profile, container, working directory) across application restarts.
*   **⌨️ Customizable Keyboard Shortcuts**: A comprehensive set of actions with highly configurable keyboard shortcuts accessible via the preferences interface.
*   **🔧 Robust User Profiles**: Create named profiles to fine-tune default containers, startup commands, appearance settings (font, palette), terminal behaviors, and compatibility modes.
*   **🛡️ `ptyxis-agent` Architecture**: A unique out-of-process helper (`ptyxis-agent`) enables full functionality even when Ptyxis is run as a Flatpak by managing PTY creation, direct container interaction, and host process monitoring.
*   **💨 High-Performance Rendering**: Leverages the VTE (Virtual Terminal Emulator) library with GPU acceleration (Vulkan/OpenGL where available) for a remarkably fluid and responsive terminal experience.
*   **🛠️ Terminal Inspector**: An integrated developer tool for debugging terminal-based applications by allowing inspection of OSC (Operating System Command) hyperlinks, mouse event coordinates, and other terminal sequences.
*   **🔒 Encrypted Scrollback Buffers**: Enhances privacy for your terminal session history.
*   **♿ Accessibility**: Designed with accessibility at its core, building upon GTK4 and VTE accessibility features to support screen readers and other assistive technologies effectively.

<div align="right">
  <a href="#ptyxis-your-container-oriented-terminal-for-gnome">Back to top ⬆️</a>
</div>

---

## 📸 Screenshots

Here's a glimpse into Ptyxis's interface and capabilities:

<div align="center">

| Feature | Screenshot |
|:---:|:---:|
| **Container Discovery & Menu** | <img src="https://gitlab.gnome.org/chergert/ptyxis/-/raw/main/data/screenshots/containers-menu.png" alt="Container Menu shows automatically discovered containers" width="400"> <br/> *Fig 2: Containers are automatically discovered and readily accessible.* |
| **Tab Overview** | <img src="https://gitlab.gnome.org/chergert/ptyxis/-/raw/main/data/screenshots/tab-overview.png" alt="Tab Overview screen shows multiple tabs with previews" width="400"> <br/> *Fig 3: A visual, searchable overview of all open terminal tabs.* |
| **Behavior Preferences** | <img src="https://gitlab.gnome.org/chergert/ptyxis/-/raw/main/data/screenshots/change-behavior.png" alt="Behavior Settings window for tweaking terminal behavior" width="400"> <br/> *Fig 4: Fine-tune various terminal behaviors to your preference.* |
| **Palette Selector** | <img src="https://gitlab.gnome.org/chergert/ptyxis/-/raw/main/data/screenshots/palette-selector.png" alt="Palette Selector screen for choosing color schemes" width="400"> <br/> *Fig 5: Select from built-in color palettes or install your own.* |
| **Profile Editor** | <img src="https://gitlab.gnome.org/chergert/ptyxis/-/raw/main/data/screenshots/edit-profile.png" alt="Profile Editor for customizing profiles" width="400"> <br/> *Fig 6: Profiles allow overriding features like default container.* |
| **Shortcut Editor** | <img src="https://gitlab.gnome.org/chergert/ptyxis/-/raw/main/data/screenshots/shortcut-editing.png" alt="Shortcut Editor for remapping keyboard shortcuts" width="400"> <br/> *Fig 7: Remap keyboard shortcuts to fit your workflow.* |
| **Sudo Process Indication** | <img src="https://gitlab.gnome.org/chergert/ptyxis/-/raw/main/data/screenshots/sudo-tracking.png" alt="Sudo Tracking indicator in the terminal" width="400"> <br/> *Fig 8: The terminal clearly indicates when you're operating as root locally.* |
| **SSH Remote Process Indication** | <img src="https://gitlab.gnome.org/chergert/ptyxis/-/raw/main/data/screenshots/ssh-tracking.png" alt="SSH Tracking indicator in the terminal" width="400"> <br/> *Fig 9: A visual cue reminds you when connected to a remote system via SSH.* |
| **Transparency Support** | <img src="https://gitlab.gnome.org/chergert/ptyxis/-/raw/main/data/screenshots/transparency.png" alt="Terminal with a partially transparent background" width="400"> <br/> *Fig 10: Optional background transparency for the daring.* |
| **Resize Indicator** | <img src="https://gitlab.gnome.org/chergert/ptyxis/-/raw/main/data/screenshots/columns-and-rows.png" alt="Terminal showing an overlay when the column or row size changes" width="400"> <br/> *Fig 11: Column and row size indicator displayed during window resizing.* |

</div>

<div align="right">
  <a href="#ptyxis-your-container-oriented-terminal-for-gnome">Back to top ⬆️</a>
</div>

---

## 🚀 Installation

### 📦 Flatpak (Recommended)

Ptyxis is primarily distributed as a Flatpak, ensuring all dependencies are managed and providing a consistent experience across Linux distributions.

*   **Stable Version (from Flathub):**
    ```bash
    flatpak install flathub app.devsuite.Ptyxis
    ```
    To run: `flatpak run app.devsuite.Ptyxis`

*   **Nightly Development Version (from GNOME Nightly):**
    For the latest features (potentially less stable):
    ```bash
    flatpak install --user --from https://nightly.gnome.org/repo/appstream/org.gnome.Ptyxis.Devel.flatpakref
    ```
    To run: `flatpak run org.gnome.Ptyxis.Devel`

### 🔨 Building from Source

Ptyxis uses the Meson build system.

1.  **Prerequisites:**
    Ensure your system has the necessary development packages installed:
    *   C compiler (e.g., GCC, Clang)
    *   Meson (version 1.0.0 or newer)
    *   Ninja
    *   GLib (version 2.80 or newer, including development headers, e.g., `libglib2.0-dev` on Debian/Ubuntu)
    *   GTK4 (version 4.14 or newer, including development headers, e.g., `libgtk-4-dev`)
    *   libadwaita (version 1.6 or newer, including development headers, e.g., `libadwaita-1-dev`)
    *   JSON-GLib (version 1.6 or newer, including development headers, e.g., `libjson-glib-dev`)
    *   VTE (GTK4 version, 0.79 or newer, including development headers, e.g., `libvte-2.91-gtk4-dev`)
    *   libportal-gtk4 (on Linux, for Flatpak portal interactions if building outside Flatpak SDK, e.g., `libportal-gtk4-dev`)

2.  **Clone the repository:**
    ```bash
    git clone https://gitlab.gnome.org/chergert/ptyxis.git
    cd ptyxis
    ```

3.  **Configure the build using Meson:**
    ```bash
    meson setup _build --prefix=/usr/local --buildtype=release # Or --buildtype=debug for development
    ```

4.  **Compile:**
    ```bash
    meson compile -C _build
    ```

5.  **Install (optional):**
    ```bash
    sudo meson install -C _build
    ```

**Using GNOME Builder:**
[GNOME Builder](https://apps.gnome.org/Builder/) provides an excellent integrated development environment for Ptyxis. Simply open the cloned `ptyxis/` directory in Builder, and it will handle the build configuration (including Flatpak SDKs if preferred) and allow you to run and debug the application.

<div align="right">
  <a href="#ptyxis-your-container-oriented-terminal-for-gnome">Back to top ⬆️</a>
</div>

---

## ⌨️ Basic Usage & Command-Line Options

Launch Ptyxis by running `ptyxis` from your system's application launcher or by typing `ptyxis` in an existing terminal (if installed to your PATH).

**Common Command-Line Options:**

*   `--version`: Show the program version (e.g., `Ptyxis 48.rc`).
*   `--preferences`: Open the preferences window directly.
*   `--new-window`: Open a new Ptyxis window, even if one is already running.
*   `--tab`: Open a new tab in the most-recently-used Ptyxis window.
*   `--tab-with-profile=PROFILE_UUID`: Open a new tab using the specified profile UUID. Profile UUIDs can be copied from `Preferences -> Profiles -> (Select Profile) -> Copy ID`.
    *   *Example:* `ptyxis --tab-with-profile=a1b2c3d4-e5f6-7890-1234-567890abcdef`
*   `-x "COMMAND"`, `--execute "COMMAND"`: Execute a custom command string in a new, standalone window.
    *   *Example:* `ptyxis -x "htop"`
*   `-- PROGRAM [ARGUMENTS...]`: Execute `PROGRAM` with its `ARGUMENTS` in a new, standalone window. The `--` signifies the end of Ptyxis options.
    *   *Example:* `ptyxis -- htop -u myuser`
*   `-d DIR`, `--working-directory DIR`: Set the working directory for a new tab/window or for a command executed with `-x` or `--`.
    *   *Example:* `ptyxis -d /home/user/myproject`
*   `--title=TITLE`: Set the initial title for a new tab or window.
*   `--maximize`: Request that a newly created window starts maximized.
*   `--fullscreen`: Request that a newly created window starts in fullscreen mode.
*   `--import-palette=FILE`: Import a Ptyxis `.palette` file into your user configuration.
*   `-s`, `--standalone`: Start a new instance of Ptyxis, ignoring any already running (useful for scripting or specific window management).
*   `-h`, `--help`: Show a summary of all available options.

For a complete list, refer to the `ptyxis(1)` man page if available on your system.

<div align="right">
  <a href="#ptyxis-your-container-oriented-terminal-for-gnome">Back to top ⬆️</a>
</div>

---

## 🏗️ Core Functionality & Design

Ptyxis utilizes a two-part architecture to provide robust terminal emulation and deep container integration, all within a modern GTK4/libadwaita user interface.

### UI Application
The user-facing component of Ptyxis is a GTK4/libadwaita application. It is responsible for:
*   Managing windows, tabs, and the overall graphical user interface.
*   Handling user profiles, theming (including color palettes and the "Window Dressing" feature), and keyboard shortcut configurations.
*   Displaying terminal content using the VTE (Virtual Terminal Emulator) widget.
*   Orchestrating communication with the `ptyxis-agent` for operations that require broader system access or interaction with container runtimes.

### `ptyxis-agent`
The `ptyxis-agent` is a distinct helper process. It typically runs on the host system, even when the Ptyxis UI application is sandboxed (e.g., as a Flatpak). Its key responsibilities include:
*   Creating and managing PTYs (pseudo-terminals) for each terminal session. This is fundamental to how terminals operate.
*   Interacting directly with various container runtimes (like Podman, Toolbox) to discover available containers and to spawn processes within them.
*   Monitoring host-level processes and retrieving system information such as the user's default shell, operating system details, and environment variables (e.g., proxy settings).
*   Facilitating secure and efficient communication with the UI application, primarily via D-Bus messages serialized over a `socketpair()`.

This separation of concerns allows the UI to remain responsive and potentially sandboxed, while the agent handles lower-level system interactions.

<div align="right">
  <a href="#ptyxis-your-container-oriented-terminal-for-gnome">Back to top ⬆️</a>
</div>

---

## 🐳 Container Integration

Ptyxis is engineered for deep and intuitive integration with local containerized development environments.

### Technical Details
1.  **Discovery:** The `ptyxis-agent` actively queries the host system to find available containers. For example, it may run commands like `podman ps --all --format=json` to list Podman containers or parse metadata from Toolbox/Distrobox. It can also monitor relevant system files (e.g., Podman's `containers.json` or its underlying database, if accessible) for dynamic updates, ensuring the list of available containers in the Ptyxis UI stays current.
2.  **Spawning:** When a user requests a terminal session within a specific container, the `ptyxis-agent` constructs and executes the appropriate command-line interface (CLI) commands for the target container runtime. Examples of such commands include:
    *   For Podman: `podman exec -it <container_id_or_name> $SHELL_OR_COMMAND`
    *   For Toolbox: `toolbox enter <container_name>`
    *   For Distrobox: `distrobox enter --no-tty <container_name> -- $SHELL_OR_COMMAND` (the `--no-tty` might be handled internally by ensuring PTY allocation is correct).
    Ptyxis, via the agent, manages PTY setup and I/O redirection to provide a seamless and interactive terminal experience within the container.
3.  **Context Management:**
    *   The active container environment for a given tab is identified using VTE terminal properties (termprops), such as `vte.container.name`. These properties are typically set by the `ptyxis-agent` upon spawning the shell within the container.
    *   The current working directory (CWD) can often be preserved or propagated into new container sessions or tabs, depending on profile settings.
    *   Selected environment variables (e.g., host proxy settings if `use-proxy` is enabled in a profile) can be passed into the container environment.
    *   User profiles allow specification of a default container for new tabs, or rules for inheriting the container context from the currently active tab.
    *   URI translation is supported for actions like "Open Link." If a URL is activated from within a container, Ptyxis attempts to open it correctly on the host system.

### `ptyxis-agent` Functions in Container Management
Beyond general PTY management, the `ptyxis-agent` is critical for container interaction:
*   It directly interfaces with container runtimes for discovery, inspection of container properties, and command execution within containers.
*   It monitors processes spawned both within containers and on the host. This includes tracking foreground processes (like `sudo` or SSH sessions that might be running inside a container session) and reporting their status and exit codes back to the UI.
*   When available and configured, the `ptyxis-agent` can create systemd user scopes for individual terminal tabs. This helps in better resource isolation and management, reducing the likelihood of the entire application being terminated by the system's Out-Of-Memory (OOM) killer due to a runaway process in a single tab.

### Supported Container Technologies
Ptyxis offers direct support for several popular local container technologies:

*   **Podman:** Full support, including automatic discovery and robust context management.
*   **Toolbox:** Well-supported for entering and managing Toolbox environments, commonly used on Fedora.
*   **Distrobox:** Supported, enabling users to seamlessly work within Distrobox-managed containerized distributions.
*   **JHBuild:** Treated as a special development environment. Commands can be automatically prefixed (e.g., with `jhbuild run ...`). For optimal JHBuild session persistence and automatic context detection in new Ptyxis tabs, add the following snippet to your shell's startup file (e.g., `~/.bashrc` or `~/.zshrc`):
    ```bash
    if [ -t 1 -a x$UNDER_JHBUILD != x ]; then
        printf "\033]777;container;push;%s;jhbuild\033\\" "JHBuild"
        function pop_container {
            printf "\033]777;container;pop;;\033\\"
        }
        trap pop_container EXIT
    fi
    ```
*   **Docker:** Direct, dedicated support for interacting with the Docker daemon (e.g., auto-discovery of Docker containers, "Open in Docker container" actions) is **not currently implemented**. Users can typically still run `docker` CLI commands within Ptyxis as they would in any other terminal. Community contributions for deeper Docker integration would be welcome.
*   **systemd-nspawn:** While not explicitly listed with the same level of auto-discovery and deep integration as Podman or Toolbox, the underlying architecture is designed to be extensible. Contributions for enhanced `systemd-nspawn` integration are welcome.

### Note on Container Security
Ptyxis is primarily designed for use in development environments and for application separation using containers. It generally assumes that the containers being interacted with are part of a trusted development workflow. Most general-purpose container runtimes, by default, may not provide sufficient hardening for all security-critical scenarios or for running untrusted workloads. Users should be aware of the security posture of their chosen container solutions and configure them appropriately for their specific security needs and threat models. Ptyxis itself does not add an extra layer of security sandboxing around these tools beyond what the tools themselves or Flatpak (if used for Ptyxis installation) provide.

<div align="right">
  <a href="#ptyxis-your-container-oriented-terminal-for-gnome">Back to top ⬆️</a>
</div>

---

## 🎨 Customization & Theming

Ptyxis offers extensive options for users to tailor its appearance and behavior:

*   **Color Palettes:**
    *   A diverse collection of built-in color schemes is provided.
    *   Palettes automatically switch between their light and dark variants in sync with the GNOME desktop's global style preference (Appearance settings).
    *   Users can install custom color palettes by placing `.palette` files in `~/.local/share/ptyxis/palettes/`. If Ptyxis is installed as a Flatpak, the path is typically `~/.var/app/app.devsuite.Ptyxis/data/ptyxis/palettes/` (for the stable version from Flathub) or `~/.var/app/org.gnome.Ptyxis.Devel/data/ptyxis/palettes/` (for the GNOME Nightly version).
    *   The "Window Dressing" feature dynamically applies accent colors from the active palette to the entire window theme, including window decorations (when supported by the desktop environment and window manager), creating a visually cohesive and integrated look.
*   **Keyboard Shortcuts:**
    *   Almost every action within Ptyxis, from opening tabs to navigating profiles, has an associated keyboard shortcut.
    *   These shortcuts are highly configurable through the Preferences interface, allowing users to rebind actions to key combinations that best suit their workflow and muscle memory.
*   **Transparency:**
    *   Optional terminal background transparency is supported. While integrated UI controls for fine-tuning transparency levels are pending future libadwaita enhancements, users can currently adjust transparency via GSettings.
    *   *Example using GSettings (replace schema ID if necessary for your installed version):*
        ```bash
        # To set 10% transparency (value from 0.0 for opaque to 1.0 for fully transparent - adjust as needed, typically lower values like 0.1-0.3 are used for slight transparency)
        gsettings set app.devsuite.Ptyxis.Settings background-transparency 0.1
        # For the nightly version, the schema might be org.gnome.Ptyxis.Devel.Settings
        # gsettings set org.gnome.Ptyxis.Devel.Settings background-transparency 0.1
        ```
*   **User Profiles:**
    *   Profiles are a cornerstone of Ptyxis customization. Users can create multiple named profiles, each with its own settings for:
        *   Default container to launch into.
        *   Custom startup commands or initial shell.
        *   Specific appearance settings (e.g., font, chosen color palette).
        *   Various terminal behaviors (e.g., scrollback limits, audible bell behavior).
        *   Robust compatibility modes tailored for different shells, remote systems, or specific terminal applications.

<div align="right">
  <a href="#ptyxis-your-container-oriented-terminal-for-gnome">Back to top ⬆️</a>
</div>

---

## ⚙️ How It Works (Agent-UI Interaction & Fallbacks)

The Ptyxis UI application and the `ptyxis-agent` communicate using D-Bus messages, which are efficiently serialized and transmitted over a `socketpair()`. This robust inter-process communication (IPC) mechanism allows the `ptyxis-agent`, which handles potentially privileged operations like PTY creation and direct container runtime interaction, to operate effectively even if it's running on the host system while the UI itself is sandboxed (e.g., when Ptyxis is installed as a Flatpak).

The `ptyxis-agent` is designed with portability as a key consideration, especially for `x86_64` architectures. It utilizes GLIBC symbol versioning, carefully selecting function versions to maintain compatibility with older Linux distributions (e.g., targeting GLIBC 2.17, which is commonly found on systems like CentOS 7 or older LTS Ubuntu releases). This ensures wider applicability of the host-agent model.

When the Ptyxis UI is run as a Flatpak application, it requests specific Flatpak permissions during installation or runtime (such as `org.freedesktop.Flatpak` which allows the use of `flatpak-spawn --host`). These permissions grant it the necessary, albeit controlled, access to the host system to spawn and communicate with its `ptyxis-agent`.

**Fallback Mechanism:** In scenarios where direct execution of the `ptyxis-agent` on the host system might fail or be undesirable—for instance, on systems with fundamentally incompatible C libraries (like Alpine Linux, which uses musl libc instead of GLIBC), or on systems with non-standard dynamic linker paths (such as NixOS where traditional `/lib` paths are managed differently)—Ptyxis incorporates a fallback strategy. It will attempt to run the `ptyxis-agent` process *within its own Flatpak sandbox*. While this fallback ensures that basic terminal functionality remains available (as PTYs can still be created within the sandbox), some host-interaction features, particularly comprehensive discovery of all host-level containers or certain types of advanced host process monitoring, might be limited or unavailable in this sandboxed-agent mode.

<div align="right">
  <a href="#ptyxis-your-container-oriented-terminal-for-gnome">Back to top ⬆️</a>
</div>

---

## 🤝 Contributing: Feature Requests and Design Changes

Ptyxis development primarily tracks engineering defects, tasks, and accepted feature requests through its [GitLab issue tracker](https://gitlab.gnome.org/chergert/ptyxis/-/issues). For proposing new features or suggesting significant design changes, please adhere to the following collaborative process:

1.  **Initiate Discussion:**
    The first step is to discuss your idea with the maintainers and the community. This can be done by:
    *   Opening an issue on the [Ptyxis GitLab issue tracker](https://gitlab.gnome.org/chergert/ptyxis/-/issues). Clearly label or title your issue as a "Discussion," "Feature Proposal," or "Idea."
    *   For substantial UI/UX changes or new interaction paradigms, it is highly recommended to create a proposal with the [GNOME Design Whiteboards project](https://gitlab.gnome.org/Teams/Design/whiteboards/) and then link this design discussion to your Ptyxis issue. This ensures alignment with broader GNOME design principles.

2.  **Develop a Specification (Especially for Larger Features):**
    A detailed specification is crucial for complex features to ensure clarity, feasibility, and a shared understanding. A good specification should ideally cover:
    *   **Problem Statement:** What user need or problem does this feature address?
    *   **Proposed Solution:** A clear description of how the feature should function from a user's perspective.
    *   **Scope and Boundaries:** What the feature *will* do, and just as importantly, what it will *not* do (non-goals).
    *   **Interaction with Existing Features:** How will this new feature affect or integrate with current Ptyxis functionalities?
    *   **Migration Strategies (if applicable):** If the feature changes existing behavior or data formats, how will existing users be affected or migrated?
    *   **UI Mock-ups or Wireframes:** Essential if the feature involves visual changes to the user interface.
    *   **Testing Strategy:** How can the feature be tested to ensure it works correctly and doesn't introduce regressions?
    *   **Potential Risks and Considerations:** Any performance implications, security concerns, or usability challenges that need to be addressed.
    *   **Implementation Ideas (Optional):** High-level thoughts on how it might be implemented technically.
    *   **Interest in Implementing:** Indicate if you (or someone else) might be interested in contributing the implementation.

Once a design or proposal is well-defined, has been discussed, and has received some initial positive feedback or refinement from the maintainers/community, a formal feature request issue can be filed (or an existing discussion issue can be updated and re-labeled appropriately) on the Ptyxis tracker. This issue should reference any design documents, whiteboard discussions, or specifications.

<div align="right">
  <a href="#ptyxis-your-container-oriented-terminal-for-gnome">Back to top ⬆️</a>
</div>

---

## 🐛 Known Issues & Troubleshooting

*   **Notifications Don't Work (e.g., for command completion):**
    For terminal notifications and certain interactive shell features (like VTE's advanced prompt integration) to function correctly, your shell environment (e.g., in `~/.bashrc`, `~/.zshrc`, or system-wide profiles like `/etc/profile`) must source the `/etc/profile.d/vte.sh` script. This script is typically provided by your distribution's VTE library package (e.g., `libvte-2.91-common` on Debian/Ubuntu systems). It sets up essential shell-side hooks and environment variables that allow the terminal emulator (VTE, and thus Ptyxis) to communicate richer status information with the running shell.
    *   **Troubleshooting:**
        1.  Verify that the `vte.sh` script exists at `/etc/profile.d/vte.sh`.
        2.  Ensure your shell's startup files (like `~/.bashrc` for bash or `~/.zshrc` for zsh) include a line to source files from `/etc/profile.d/` or specifically source `vte.sh`. Some shells do this automatically if `/etc/profile` is sourced.
        3.  If using a custom shell or a minimal environment, you might need to manually add: `if [ -f /etc/profile.d/vte.sh ]; then . /etc/profile.d/vte.sh; fi` to your shell's rc file.

*   **GPU/Font Rendering Issues:**
    Problems related to GPU-accelerated rendering artifacts (glitches, incorrect colors, performance drops) or unusual font rendering (e.g., incorrect spacing, clipping, blurriness, especially with HiDPI scaling like 200%) are often rooted in the underlying GTK or VTE libraries, or occasionally in graphics drivers or Wayland compositor interactions.
    *   **Troubleshooting & Reporting:**
        1.  Try disabling GPU acceleration in VTE if such an option becomes available via GSettings or an environment variable (consult VTE documentation for current methods).
        2.  Test with different fonts or font rendering settings in GNOME Tweaks or your desktop environment's settings.
        3.  If the issue persists and seems related to the core rendering libraries, it's generally best to report such issues directly to the respective upstream projects, providing as much detail as possible:
            *   [GNOME/gtk Issues](https://gitlab.gnome.org/GNOME/gtk/-/issues)
            *   [GNOME/vte Issues](https://gitlab.gnome.org/GNOME/vte/-/issues)
        4.  When reporting, include: Ptyxis version, GTK version, VTE version, Linux distribution, graphics card & driver version, display scaling factor, and precise steps to reproduce the issue.

*   **Container Detection for `toolbox`, `podman`, `distrobox`:**
    Optimal automatic detection of containers and reliable context propagation (knowing which container a tab is in) relies on these container tools emitting specific VTE escape sequences (like OSC 777) to inform the terminal emulator about the current container environment.
    *   **Troubleshooting:**
        1.  Ensure you are using **recent versions** of `toolbox`, `podman`, and `distrobox`, as older versions might not have this capability fully implemented or enabled by default on all Linux distributions.
        2.  Check the documentation for your specific container tool and distribution for any configuration needed to enable VTE integration or prompt notifications.
        3.  If automatic detection fails consistently for a specific container, you can often manually achieve the desired container session by creating a dedicated profile in Ptyxis that explicitly launches commands within your target container environment (e.g., profile command: `podman start -ai my_container_name`).

<div align="right">
  <a href="#ptyxis-your-container-oriented-terminal-for-gnome">Back to top ⬆️</a>
</div>

---

## 📜 License

Ptyxis is open-source software licensed under the terms of the **GNU General Public License v3.0 or later (GPL-3.0+)**.
A copy of the license is included in the source code repository in the `COPYING` file, which can typically be found at [https://gitlab.gnome.org/chergert/ptyxis/-/blob/main/COPYING](https://gitlab.gnome.org/chergert/ptyxis/-/blob/main/COPYING).

<div align="right">
  <a href="#ptyxis-your-container-oriented-terminal-for-gnome">Back to top ⬆️</a>
</div>

---

## 🙏 Acknowledgments

Ptyxis is primarily developed by **Christian Hergert**. Its creation represents an evolution of terminal workspace concepts initially prototyped within [GNOME Builder](https://apps.gnome.org/app/org.gnome.Builder/). The project was significantly motivated by recent performance optimizations and feature enhancements in the VTE (Virtual Terminal Emulator) library, particularly those beneficial for the Wayland display server environment. The overarching aim is to provide a fast, feature-rich, and deeply container-aware terminal experience specifically tailored for the GNOME desktop.

<div align="right">
  <a href="#ptyxis-your-container-oriented-terminal-for-gnome">Back to top ⬆️</a>
</div>