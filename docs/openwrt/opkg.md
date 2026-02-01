---
title: opkg
status: draft
---

`opkg` is the package manager in OpenWrt, similar to `apt` on Debian/Ubuntu or `yum` on CentOS. It allows you to **install, remove, update, and manage software packages** on your router.

------

## **1. Checking if `opkg` is available**

On your OpenWrt router, open SSH and type:

```bash
opkg --help
```

If `opkg` is installed, you’ll see a list of commands and options.

------

## **2. Updating package lists**

Before installing anything, always update the list of available packages:

```bash
opkg update
```

-   This downloads the latest package information from OpenWrt repositories.
-   **Important**: Run this every time you want to install new software to ensure you get the latest version.

------

## **3. Searching for packages**

You can search for packages by name or description:

```bash
opkg list | grep <keyword>
```

Example: search for `usb` packages:

```bash
opkg list | grep usb
```

-   `opkg list` shows all packages.
-   `grep usb` filters the list to only lines containing `usb`.

------

## **4. Installing a package**

To install a package:

```bash
opkg install <package-name>
```

Example: install USB support:

```bash
opkg install kmod-usb-storage
```

-   Most OpenWrt packages have dependencies. `opkg` will install them automatically.
-   Some common packages:
    -   `luci` – Web interface
    -   `kmod-usb-storage` – USB storage support
    -   `nano` – Lightweight text editor

------

## **5. Removing a package**

To remove a package you no longer need:

```bash
opkg remove <package-name>
```

Example:

```bash
opkg remove nano
```

-   Use `--force-depends` if you need to remove a package that is required by another (use carefully!).

------

## **6. Upgrading packages**

To upgrade **all installed packages**:

```bash
opkg list-upgradable       # List packages that can be upgraded
opkg upgrade               # Upgrade them
```

⚠️ **Warning:** Upgrading all packages on a router with limited flash storage can sometimes fail. Upgrade selectively if needed.

------

## **7. Showing package info**

To check details about a package:

```bash
opkg info <package-name>
```

Example:

```bash
opkg info kmod-usb-storage
```

This shows version, description, dependencies, and installed status.

------

## **8. Advanced tips**

1.  **Saving storage space**

    -   OpenWrt routers have limited flash. Check installed packages:

    ```bash
    opkg list-installed
    ```

2.  **Working with feeds**

    -   Some packages require extra feeds. Feeds are additional sources of packages.
    -   Configure in `/etc/opkg/customfeeds.conf`.

3.  **Installing packages from `.ipk` files**

    -   You can download `.ipk` files and install locally:

    ```bash
    opkg install /tmp/mypackage.ipk
    ```

------

## **9. Example Workflow: USB + SD Card Support**

1.  Update package list:

```bash
opkg update
```

1.  Install kernel modules for USB & SD cards:

```bash
opkg install kmod-usb-storage kmod-fs-ext4 block-mount
```

1.  Install utilities for mounting:

```bash
opkg install mount-utils fdisk lsblk
```

1.  Verify:

```bash
ls /dev/sd*
```

------

## **10. Summary of Common `opkg` Commands**

| Command                | Purpose                     |
| ---------------------- | --------------------------- |
| `opkg update`          | Update package list         |
| `opkg list`            | List all available packages |
| `opkg list-installed`  | List installed packages     |
| `opkg install <pkg>`   | Install a package           |
| `opkg remove <pkg>`    | Remove a package            |
| `opkg info <pkg>`      | Show package info           |
| `opkg upgrade`         | Upgrade installed packages  |
| `opkg list-upgradable` | List upgradable packages    |

