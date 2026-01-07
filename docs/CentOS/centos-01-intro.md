# CentOS-01: Intro

## 1. What Is CentOS?

**CentOS (Community ENTerprise Operating System)** is a **free, open-source Linux distribution** that is built from the same source code as **Red Hat Enterprise Linux (RHEL)**.

In simple terms:

-   **RHEL** → paid, enterprise support
-   **CentOS** → free, community version of RHEL

Because of this, CentOS is:

-   Very **stable**
-   Widely used on **servers**
-   Popular for **learning Linux system administration**

>   If you learn CentOS, you can easily work with RHEL and many cloud servers.

------

## 2. CentOS Versions (Important for Beginners)

### 2.1 CentOS Linux (Traditional)

-   Versions like **CentOS 7**
-   Very stable
-   Common in tutorials and older servers
-   **CentOS 7 is still widely used**

### 2.2 CentOS Stream (New Model)

-   Rolling-release, sits **between Fedora and RHEL**
-   Receives updates earlier than RHEL
-   More “preview” style

👉 **For beginners:**
If you see *CentOS 7*, it is perfectly fine to learn with it.

------

## 3. Where Is CentOS Used?

CentOS is mainly used in:

-   Web servers (Apache / Nginx)
-   Database servers (MySQL, PostgreSQL)
-   Big data (Hadoop, Spark)
-   DevOps / CI systems
-   Cloud & virtual machines

You usually **do not install CentOS on laptops**.
It’s mostly used on **servers or virtual machines**.

------

## 4. Basic CentOS Concepts You Must Know

### 4.1 Linux Is Case-Sensitive

```bash
File.txt ≠ file.txt
```

### 4.2 Everything Is a File

-   Devices
-   Disks
-   Network
-   Processes

All are represented as files in Linux.

------

## 5. Logging into CentOS

Usually you connect via **SSH**:

```bash
ssh username@server_ip
```

After login, you’ll see a shell prompt like:

```bash
[user@localhost ~]$
```

------

## 6. Basic File and Directory Commands

### 6.1 Where Am I?

```bash
pwd
```

### 6.2 List Files

```bash
ls
ls -l
ls -a
```

### 6.3 Change Directory

```bash
cd /etc
cd ~
cd ..
```

### 6.4 Create Files and Directories

```bash
touch file.txt
mkdir mydir
```

### 6.5 Copy, Move, Delete

```bash
cp a.txt b.txt
mv a.txt dir/
rm a.txt
rm -r mydir
```

⚠️ **Be careful with `rm -r`** — no recycle bin.

------

## 7. Viewing File Contents

### 7.1 View Text Files

```bash
cat file.txt
less file.txt
```

### 7.2 View Logs

```bash
less /var/log/messages
```

Press:

-   `q` → quit
-   `/text` → search

------

## 8. Package Management (Very Important)

CentOS uses **yum** (CentOS 7) or **dnf** (newer).

### 8.1 Install Software

```bash
sudo yum install vim
```

### 8.2 Remove Software

```bash
sudo yum remove vim
```

### 8.3 Update System

```bash
sudo yum update
```

------

## 9. User and Permission Basics

### 9.1 Root vs Normal User

-   **root** → super administrator
-   normal user → limited permissions

Use `sudo` to run admin commands:

```bash
sudo systemctl status sshd
```

### 9.2 File Permissions

```bash
ls -l
```

Example:

```text
-rw-r--r-- 1 user user file.txt
```

Meaning:

-   owner can read/write
-   group can read
-   others can read

------

## 10. Service Management (systemctl)

CentOS uses **systemd**.

### 10.1 Check Service Status

```bash
systemctl status sshd
```

### 10.2 Start / Stop / Restart

```bash
sudo systemctl start nginx
sudo systemctl stop nginx
sudo systemctl restart nginx
```

### 10.3 Enable at Boot

```bash
sudo systemctl enable nginx
```

------

## 11. Network Basics

### 11.1 Check IP Address

```bash
ip addr
```

### 11.2 Test Connectivity

```bash
ping google.com
```

------

## 12. Firewall (firewalld)

### 12.1 Check Firewall Status

```bash
sudo systemctl status firewalld
```

### 12.2 Open a Port (Example: 80)

```bash
sudo firewall-cmd --add-port=80/tcp --permanent
sudo firewall-cmd --reload
```

------

## 13. Logs and Troubleshooting

Important log locations:

```text
/var/log/messages
/var/log/secure
/var/log/boot.log
```

Check logs first when something goes wrong.

------

## 14. Common Beginner Mistakes

-   Forgetting `sudo`
-   Using `rm -rf /` (never do this!)
-   Editing system files without backup
-   Confusing CentOS with Ubuntu commands (`apt` ≠ `yum`)

------

## 15. What to Learn Next?

After this tutorial, a good learning path is:

1.  Vim basics
2.  Shell scripting
3.  SSH configuration
4.  Nginx / Apache
5.  MySQL / PostgreSQL
6.  Docker & containers

------

## 16. Summary

CentOS is:

-   Stable
-   Server-oriented
-   Perfect for learning Linux administration

If you understand:

-   file operations
-   package management
-   services
-   permissions

👉 You already have **solid Linux fundamentals**.