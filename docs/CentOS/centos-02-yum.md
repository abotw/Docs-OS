# CentOS-02: YUM

## 1. What Is YUM?

**YUM (Yellowdog Updater, Modified)** is the **package manager** used in CentOS 7.

In simple words:

>   **YUM helps you install, update, remove, and manage software automatically.**

Instead of downloading `.rpm` files manually, YUM:

-   Downloads software from repositories
-   Resolves dependencies automatically
-   Keeps your system consistent and safe

------

## 2. What Is a Package?

A **package** is a software bundle that contains:

-   Program files
-   Libraries
-   Configuration files
-   Version information

In CentOS, packages are usually:

```text
*.rpm
```

YUM works with RPM packages but **you should use YUM, not rpm**, in daily work.

------

## 3. YUM Basics You Must Know

### 3.1 Root Permission Required

Most YUM commands need **root** privileges:

```bash
sudo yum install vim
```

Or switch to root:

```bash
su -
```

------

## 4. Common YUM Commands (Most Important)

### 4.1 Install a Package

```bash
sudo yum install vim
```

YUM will:

1.  Check repositories
2.  Resolve dependencies
3.  Ask for confirmation

Type `y` and press Enter.

------

### 4.2 Remove a Package

```bash
sudo yum remove vim
```

------

### 4.3 Update All Packages

```bash
sudo yum update
```

Update a single package:

```bash
sudo yum update nginx
```

------

### 4.4 Search for a Package

```bash
yum search nginx
```

------

### 4.5 Get Package Information

```bash
yum info nginx
```

------

## 5. List Packages

### 5.1 List Installed Packages

```bash
yum list installed
```

### 5.2 List Available Packages

```bash
yum list available
```

### 5.3 Check if a Package Is Installed

```bash
yum list installed | grep nginx
```

------

## 6. YUM Repositories (Very Important Concept)

### 6.1 What Is a Repository?

A **repository (repo)** is a server that stores:

-   Software packages
-   Metadata
-   Dependency information

YUM downloads software **only from enabled repositories**.

------

### 6.2 Repo Configuration Location

```bash
/etc/yum.repos.d/
```

Each file ends with:

```text
.repo
```

Example:

```text
CentOS-Base.repo
```

------

### 6.3 View Enabled Repositories

```bash
yum repolist
```

------

## 7. Install Extra Repositories (Common Task)

### 7.1 EPEL Repository

**EPEL (Extra Packages for Enterprise Linux)** provides many useful tools.

Install EPEL:

```bash
sudo yum install epel-release
```

Then:

```bash
yum repolist
```

### 7.2 Aliyun Mirrors

```shell
cd /etc/yum.repos.d
# 1. Backup original
mv CentOS-Base.repo CentOS-Base.repo.backup
# 2. Download new source
wget http://mirrors.aliyun.com/repo/Centos-7.repo
# 3. Set as default
mv Centos-7.repo CentOS-Base.repo
```

------

## 8. Clean YUM Cache

Sometimes YUM has problems due to cache.

### 8.1 Clean Cache

```bash
sudo yum clean all
```

### 8.2 Rebuild Cache

```bash
sudo yum makecache
```

------

## 9. Install from a Local RPM File

If you already have an `.rpm` file:

```bash
sudo yum install ./package.rpm
```

YUM will still handle dependencies (better than `rpm -ivh`).

------

## 10. YUM History (Very Useful)

### 10.1 View History

```bash
yum history
```

### 10.2 Undo a Transaction

```bash
sudo yum history undo 10
```

This can **undo an install or update** safely.

------

## 11. YUM Groups (Optional but Helpful)

### 11.1 List Groups

```bash
yum group list
```

### 11.2 Install a Group

```bash
sudo yum groupinstall "Development Tools"
```

------

## 12. Common Errors and Fixes

### 12.1 “Cannot find a valid baseurl”

-   Network issue
-   DNS problem
-   Repo misconfiguration

Check:

```bash
ping google.com
```

------

### 12.2 Locked YUM Process

```bash
ps aux | grep yum
```

Then wait or kill the process.

------

## 13. Best Practices for Beginners

✅ Use `yum` instead of `rpm`
✅ Update system regularly
✅ Install EPEL early
✅ Read confirmation messages carefully
❌ Don’t disable core repositories blindly

------

## 14. YUM vs DNF (Quick Note)

| Feature             | YUM      | DNF       |
| ------------------- | -------- | --------- |
| Used in             | CentOS 7 | CentOS 8+ |
| Dependency handling | Good     | Better    |
| Speed               | Slower   | Faster    |

If you know YUM, learning DNF is very easy.

------

## 15. Summary

YUM helps you:

-   Install software
-   Remove software
-   Update your system
-   Manage dependencies
-   Work safely and efficiently

**Essential commands to remember:**

```bash
yum install
yum remove
yum update
yum search
yum info
yum repolist
```

