# WSL

## **1. What is WSL?**

WSL lets you run a **Linux environment directly on Windows** without a virtual machine.
You can run Linux command-line tools, utilities, and applications **natively**, side by side with Windows.

-   **No dual-boot needed.**
-   **No heavy VM overhead.**
-   Ideal for developers, sysadmins, or anyone who needs Linux commands/tools on Windows.

There are two versions:

| Version   | Features                                                     |
| --------- | ------------------------------------------------------------ |
| **WSL 1** | Uses a translation layer. Fast for file-heavy tasks in Windows filesystem. |
| **WSL 2** | Uses a real Linux kernel inside a lightweight VM. Better compatibility and performance for Linux apps. |

>   Tip: **WSL 2 is recommended** for most users.

------

## **2. Prerequisites**

-   Windows 10 (Version 2004 or later) or Windows 11.
-   Administrator privileges on your PC.
-   Internet connection to download Linux distributions.

------

## **3. Installing WSL**

Open **PowerShell** as Administrator and run:

```powershell
wsl --install
```

What this does:

1.  Enables WSL feature.
2.  Installs the **WSL 2 kernel**.
3.  Sets WSL 2 as default.
4.  Installs **Ubuntu** by default (can choose other distros later).

>   After installation, restart your PC if prompted.

------

## **4. Check WSL Installation**

After reboot, open PowerShell (not necessarily as admin) and run:

```powershell
wsl --list --verbose
```

Example output:

```
  NAME      STATE           VERSION
* Ubuntu    Running         2
```

-   `VERSION 2` → WSL 2 is running.
-   `STATE` → whether your Linux distro is running.

------

## **5. Launching Linux**

-   Open **Windows Terminal** or **PowerShell**, type:

```powershell
wsl
```

-   You’ll enter a Linux shell. Example:

```
user@DESKTOP:~$
```

-   Or, open **Ubuntu** from the Start Menu (installed distro appears as a Windows app).

------

## **6. Common WSL Commands**

| Command                         | Description                                                 |
| ------------------------------- | ----------------------------------------------------------- |
| `wsl`                           | Launches default Linux distro.                              |
| `wsl -l -v`                     | Lists installed distros with version info.                  |
| `wsl --install -d <DistroName>` | Install a specific distro, e.g., `wsl --install -d Debian`. |
| `wsl --set-default-version 2`   | Set WSL 2 as default for new distros.                       |
| `wsl --unregister <DistroName>` | Uninstall a distro.                                         |

------

## **7. File System Access**

-   **Windows drives in Linux**:

```bash
cd /mnt/c
ls
```

-   **Linux files from Windows**: Open File Explorer and go to:

```
\\wsl$\Ubuntu\
```

>   This path shows your Linux filesystem.

------

## **8. Installing Linux Tools**

Once inside WSL, you can use Linux package managers like `apt`:

```bash
sudo apt update        # Update package lists
sudo apt upgrade -y    # Upgrade installed packages
sudo apt install git   # Install Git
```

>   Works just like a normal Linux system.

------

## **9. Running Linux & Windows Together**

-   Run Windows apps from Linux:

```bash
notepad.exe
explorer.exe .
```

-   Run Linux commands from Windows PowerShell:

```powershell
wsl ls -la
```

>   This lets you mix Linux and Windows workflows seamlessly.

------

## **10. Switching Between WSL Versions**

Check current version:

```powershell
wsl -l -v
```

Set a distro to WSL 2:

```powershell
wsl --set-version Ubuntu 2
```

Set WSL 1 if needed:

```powershell
wsl --set-version Ubuntu 1
```

------

## **11. Tips & Tricks**

-   **Update WSL kernel manually**:

```powershell
wsl --update
```

-   **Backup/Export a distro**:

```powershell
wsl --export Ubuntu ubuntu_backup.tar
```

-   **Import a distro**:

```powershell
wsl --import UbuntuBackup C:\WSL\UbuntuBackup ubuntu_backup.tar --version 2
```

-   **Use multiple distros**: You can install Ubuntu, Debian, Fedora, etc., side by side.

------

## **12. Resources for Beginners**

-   [Official WSL Docs](https://learn.microsoft.com/en-us/windows/wsl/)
-   [Windows Terminal](https://aka.ms/terminal) for a better experience.
-   Tutorials on Linux basics (`bash`, `vim`, `git`) since WSL gives you the Linux shell.

------

## Summary

-   WSL gives you Linux on Windows without a VM.
-   WSL 2 is recommended.
-   Linux tools, files, and Windows apps can work together seamlessly.
-   Easy to install, manage, and switch distros.