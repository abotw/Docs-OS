# rpm

## 1. What is `rpm`?

`rpm` stands for **RPM Package Manager**.

It is a **low-level package management tool** used mainly on:

-   RHEL
-   CentOS
-   Rocky Linux
-   AlmaLinux
-   Fedora

`rpm` is used to:

-   Install `.rpm` software packages
-   Query package information
-   Verify installed packages
-   Remove packages

>   📌 `rpm` works **directly with local `.rpm` files**
>   It does **NOT** automatically resolve dependencies.

------

## 2. What Is an RPM Package?

An RPM package is a file like:

```text
httpd-2.4.57-1.el9.x86_64.rpm
```

It contains:

-   Compiled binaries
-   Configuration files
-   Metadata (version, dependencies, description)
-   Scripts (pre/post install)

------

## 3. Basic Syntax

```bash
rpm [options] package
```

Examples:

```bash
rpm -ivh package.rpm
rpm -qa
rpm -qi bash
```

------

## 4. Install an RPM Package

### 4.1 Install from a Local File (`-i`)

```bash
rpm -ivh httpd.rpm
```

Options:

-   `-i` → install
-   `-v` → verbose
-   `-h` → progress bar

------

### 4.2 Upgrade or Install (`-U`)

```bash
rpm -Uvh httpd.rpm
```

✔ Recommended over `-i`
✔ Upgrades if installed, installs if not

------

## 5. Remove an RPM Package

```bash
rpm -e httpd
```

-   `-e` → **e**rase

>   Use **package name**, not file name.

## 6. Query Installed Packages

### 6.1 List All Installed Packages

```bash
rpm -qa
```

Options:

-   `-q` → **q**uery
-   `-a` → **a**ll

### 6.2 Query a Specific Package

```bash
rpm -qi bash
```

------

### 6.3 List Files Installed by a Package

```bash
rpm -ql bash
```

------

### 6.4 Find Which Package Owns a File

```bash
rpm -qf /bin/ls
```

------

## 7. Query an RPM File (Not Installed)

### Package Info

```bash
rpm -qip nginx.rpm
```

------

### List Files in an RPM File

```bash
rpm -qlp nginx.rpm
```

------

## 8. Check Dependencies

### Show Required Dependencies

```bash
rpm -qpR nginx.rpm
```

------

### Show What a Package Provides

```bash
rpm -q --provides bash
```

------

## 9. Verify Installed Packages

```bash
rpm -V bash
```

Checks:

-   File size
-   Permissions
-   Ownership
-   Checksum

No output = everything OK.

------

## 10. Common `rpm` Options Summary

| Option   | Meaning            |
| -------- | ------------------ |
| `-i`     | Install            |
| `-U`     | Upgrade or install |
| **`-e`** | **e**rase          |
| `-q`     | **q**uery          |
| `-a`     | **a**ll packages   |
| `-l`     | List files         |
| `-f`     | File owner         |
| `-p`     | Query RPM file     |
| `-V`     | Verify             |
| `-h`     | Progress bar       |

------

## 11. Typical Beginner Workflow

### Install Software from RPM

```bash
rpm -Uvh app.rpm
```

If dependency error appears:

```text
failed dependencies:
```

➡️ Use `yum` / `dnf` instead.

------

### Check Installation

```bash
rpm -qi app
rpm -ql app
```

------

### Remove Software

```bash
rpm -e app
```

------

## 12. `rpm` vs `yum` / `dnf`

| Feature               | rpm   | yum / dnf |
| --------------------- | ----- | --------- |
| Dependency resolution | ❌ No  | ✅ Yes     |
| Install from repo     | ❌ No  | ✅ Yes     |
| Install local file    | ✅ Yes | ✅ Yes     |
| Low-level control     | ✅ Yes | ❌ Limited |

>   📌 Use `rpm` to **inspect** packages
>   📌 Use `yum` / `dnf` to **install software**

------

## 13. Common Beginner Mistakes ⚠️

### ❌ Using RPM File Name When Removing

```bash
rpm -e httpd.rpm   # WRONG
```

### ✅ Correct

```bash
rpm -e httpd
```

------

### ❌ Ignoring Dependencies

```bash
rpm -ivh app.rpm
```

Fails if dependencies are missing.

## 14. Practical Examples

### Check if a Package Is Installed

```bash
rpm -q openssh
```

------

### Find Config Files

```bash
rpm -qc httpd
```

------

### Find Documentation Files

```bash
rpm -qd bash
```

------

## 15. Quick Cheat Sheet

```bash
rpm -qa
rpm -qi pkg
rpm -ql pkg
rpm -qf file
rpm -Uvh pkg.rpm
rpm -e pkg --nodeps
```

------

## 16. Summary

-   `rpm` is a **low-level package manager**
-   Works with `.rpm` files
-   Does **not** resolve dependencies
-   Best used for querying and inspecting packages
-   Prefer `yum` / `dnf` for real installations