# Ubuntu-01: Intro

## 1. What Is Ubuntu?

**Ubuntu** is a popular **Linux operating system** based on **Debian**.
It is:

-   ✅ Free and open-source
-   ✅ Stable and secure
-   ✅ Widely used on **desktops, servers, cloud, and Raspberry Pi**
-   ✅ Backed by **Canonical**

Ubuntu is often recommended for beginners because it is easy to install, well documented, and has a huge community.

------

## 2. Ubuntu Editions

Ubuntu comes in several flavors:

### 2.1 Ubuntu Desktop

-   Graphical interface (GUI)
-   Suitable for daily use, study, and development
-   Default desktop environment: **GNOME**

### 2.2 Ubuntu Server

-   No GUI by default
-   Used for servers, cloud, containers
-   Managed via **command line + SSH**

### 2.3 Ubuntu LTS vs Interim Releases

| Type                    | Example   | Support  |
| ----------------------- | --------- | -------- |
| LTS (Long Term Support) | 22.04 LTS | 5 years  |
| Interim                 | 23.10     | 9 months |

👉 **Beginners should always choose LTS**.

------

## 3. Basic Ubuntu Desktop Layout

On Ubuntu Desktop, you’ll see:

-   **Top Bar**
    -   System status (network, sound, battery)
    -   Date & time
-   **Dock (left side)**
    -   Pinned applications
-   **Activities Overview**
    -   Press `Super` (Windows key)
    -   Search apps and files

------

## 4. Ubuntu File System Basics

Linux does not use drive letters like `C:` or `D:`.

### 4.1 Important Directories

| Directory          | Purpose                    |
| ------------------ | -------------------------- |
| `/`                | Root of the system         |
| `/home`            | User home directories      |
| `/home/username`   | Your personal files        |
| `/etc`             | System configuration       |
| `/bin`, `/usr/bin` | Commands                   |
| `/var`             | Logs, cache, variable data |

👉 Your files live in **`/home/yourname`**.

------

## 5. Package Management (Very Important)

Ubuntu uses **APT** to install software.

### 5.1 Update Software List

```bash
sudo apt update
```

### 5.2 Upgrade Installed Software

```bash
sudo apt upgrade
```

### 5.3 Install Software

```bash
sudo apt install git
```

### 5.4 Remove Software

```bash
sudo apt remove git
```

-   `sudo` = run as administrator
-   Ubuntu software comes from **repositories**

------

## 6. Terminal Basics

The **Terminal** is a powerful tool in Ubuntu.

### 6.1 Open Terminal

-   Press `Ctrl + Alt + T`

### 6.2 Common Commands

| Command      | Meaning                |
| ------------ | ---------------------- |
| `pwd`        | Show current directory |
| `ls`         | List files             |
| `cd dir`     | Change directory       |
| `mkdir test` | Create directory       |
| `rm file`    | Delete file            |
| `cp a b`     | Copy                   |
| `mv a b`     | Move / rename          |

Example:

```bash
cd ~/Documents
ls
```

------

## 7. Users and Permissions

Linux is **multi-user** by design.

### 7.1 File Permissions

```bash
ls -l
```

Example output:

```
-rw-r--r-- 1 user user file.txt
```

Meaning:

-   `r` = read
-   `w` = write
-   `x` = execute

### 7.2 Why `sudo` Exists

-   Protects the system
-   Prevents accidental damage

------

## 8. Software Installation Methods

Ubuntu supports multiple ways:

1.  **APT (recommended)**

2.  **Snap**

    ```bash
    snap install code
    ```

3.  **AppImage**

4.  **.deb packages**

    ```bash
    sudo dpkg -i package.deb
    ```

👉 Beginners should prefer **APT or Snap**.

------

## 9. Networking Basics

### 9.1 Check IP Address

```bash
ip a
```

### 9.2 Test Network

```bash
ping google.com
```

### 9.3 SSH (Remote Login)

```bash
ssh user@ip_address
```

Common in servers and Raspberry Pi usage.

------

## 10. Updating the System (Best Practice)

Regularly run:

```bash
sudo apt update && sudo apt upgrade
```

This keeps your system:

-   Secure
-   Stable
-   Bug-free

------

## 11. Getting Help

### 11.1 Manual Pages

```bash
man ls
```

### 11.2 Built-in Help

```bash
ls --help
```

### 11.3 Community

-   Ask Ubuntu
-   Ubuntu Wiki
-   GitHub issues

------

## 12. Who Should Use Ubuntu?

Ubuntu is great for:

-   Students learning Linux
-   Developers
-   Servers & cloud
-   Raspberry Pi users
-   Daily desktop users

------

## 13. Learning Path Recommendation

For beginners:

1.  Learn basic terminal commands
2.  Understand file system & permissions
3.  Learn package management
4.  Learn networking & SSH
5.  Move to shell scripting

