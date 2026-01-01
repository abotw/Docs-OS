# XDG on Linux

## 1. What is XDG?

**XDG** stands for **X Desktop Group** (now under **freedesktop.org**).

In simple terms:

>   **XDG defines a set of standards that help Linux applications know *where to store files* and *how to integrate with the desktop environment*.**

Before XDG, every application put files wherever it wanted, which led to chaos in `$HOME`. XDG brings order.

## 2. Why XDG Exists

Without XDG:

-   Config files scattered everywhere (`~/.app1`, `~/.config2`, `~/random`)
-   Cache files mixed with important data
-   Desktop menus inconsistent across environments

With XDG:

-   Predictable directories
-   Cleaner home directory
-   Desktop-agnostic behavior (works on GNOME, KDE, XFCE, etc.)

## 3. The Core Idea: XDG Base Directory Specification

The **XDG Base Directory Specification** defines **standard environment variables** that applications should follow.

### The Most Important XDG Variables

| Variable          | Purpose                     | Default Location |
| ----------------- | --------------------------- | ---------------- |
| `XDG_CONFIG_HOME` | User configuration files    | `~/.config`      |
| `XDG_DATA_HOME`   | User data files             | `~/.local/share` |
| `XDG_CACHE_HOME`  | Cache files                 | `~/.cache`       |
| `XDG_STATE_HOME`  | State files (logs, history) | `~/.local/state` |

If these variables are **not set**, applications must fall back to the defaults above.

## 4. What Goes Where? (Very Important)

### 4.1 Configuration → `XDG_CONFIG_HOME`

-   Settings you want to keep
-   Human-readable
-   Safe to back up

Example:

```text
~/.config/
 ├── git/config
 ├── nvim/init.lua
 └── alacritty/alacritty.yml
```

------

### 4.2 Data → `XDG_DATA_HOME`

-   Persistent user data
-   Databases, icons, plugins

Example:

```text
~/.local/share/
 ├── applications/
 ├── fonts/
 └── nvim/site/
```

------

### 4.3 Cache → `XDG_CACHE_HOME`

-   Temporary data
-   Safe to delete

Example:

```text
~/.cache/
 ├── pip/
 ├── thumbnails/
 └── chromium/
```

------

### 4.4 State → `XDG_STATE_HOME`

-   Logs, history, runtime state
-   Not exactly config, not exactly cache

Example:

```text
~/.local/state/
 ├── bash/history
 └── nvim/log
```

## 5. Viewing Your XDG Settings

Check current values:

```bash
echo $XDG_CONFIG_HOME
echo $XDG_DATA_HOME
echo $XDG_CACHE_HOME
```

If nothing prints, defaults are being used.

## 6. Setting XDG Variables (Optional)

You can customize XDG directories in your shell config:

```bash
# ~/.bashrc or ~/.zshrc
export XDG_CONFIG_HOME="$HOME/.config"
export XDG_DATA_HOME="$HOME/.local/share"
export XDG_CACHE_HOME="$HOME/.cache"
export XDG_STATE_HOME="$HOME/.local/state"
```

💡 Most users keep defaults — changing them is optional.

## 7. XDG and Applications

### Good Citizens (Follow XDG)

-   `git`
-   `neovim`
-   `systemd`
-   `pip`
-   `flatpak`

### Bad / Legacy Apps

-   Still write to `~/.appname`
-   Ignore XDG variables

You’ll often see people migrate old dotfiles into `~/.config`.

## 8. XDG Desktop Integration (Quick Intro)

Beyond directories, XDG also defines:

### `.desktop` files

Used for application launchers.

Location:

```text
~/.local/share/applications/
```

Example:

```ini
[Desktop Entry]
Name=My App
Exec=my-app
Type=Application
```

### MIME types & default apps

Managed via:

```bash
xdg-mime
xdg-open
```

Example:

```bash
xdg-open file.pdf
```

This opens the file using your system’s default app.

## 9. Common XDG Tools You’ll See

| Command         | Purpose                           |
| --------------- | --------------------------------- |
| `xdg-open`      | Open file/URL with default app    |
| `xdg-mime`      | Query/set default applications    |
| `xdg-user-dirs` | Manage Documents, Downloads, etc. |

Example:

```bash
xdg-user-dir DOCUMENTS
```

## 10. Why XDG Matters to You

If you:

-   Manage dotfiles
-   Write Linux apps
-   Use multiple desktop environments
-   Care about clean `$HOME`

Then **understanding XDG is essential**.

## 11. One-Sentence Summary

>   **XDG is a Linux standard that tells applications where to store config, data, cache, and how to integrate with the desktop in a clean, predictable way.**

