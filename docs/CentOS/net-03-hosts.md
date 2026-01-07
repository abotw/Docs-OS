# CentOS: Hosts

Understanding `/etc/hosts`

## 1. What Is `/etc/hosts`?

`/etc/hosts` is a **local hostname resolution file**.

In simple words:

>   It maps **IP addresses to hostnames** *before* the system asks a DNS server.

When your system tries to access a hostname (for example `example.com`), it:

1.  Checks `/etc/hosts`
2.  If not found, queries DNS

------

## 2. Why Does `/etc/hosts` Exist?

`/etc/hosts` is used for:

-   Quick hostname resolution
-   Testing without DNS
-   Local development
-   Temporary overrides
-   Small internal networks

It works **without internet access**.

------

## 3. Where Is `/etc/hosts` Located?

```text
/etc/hosts
```

It is a **plain text file**.

------

## 4. Typical `/etc/hosts` File Example

```text
127.0.0.1   localhost localhost.localdomain
::1         localhost localhost.localdomain

192.168.1.10  webserver
192.168.1.20  dbserver
```

------

## 5. Basic Format of `/etc/hosts`

Each line follows this format:

```text
IP_address   hostname [alias1 alias2 ...]
```

Important rules:

-   Fields are separated by **spaces or tabs**
-   One IP can map to **multiple names**
-   Lines starting with `#` are comments

------

## 6. Important Default Entries

### 6.1 Loopback Address

```text
127.0.0.1 localhost
```

-   Refers to **your own machine**
-   Used for local services

IPv6 equivalent:

```text
::1 localhost
```

------

## 7. How `/etc/hosts` Works (Order Matters)

Linux hostname resolution order is defined in:

```text
/etc/nsswitch.conf
```

Typical entry:

```text
hosts: files dns
```

Meaning:

1.  `files` → `/etc/hosts`
2.  `dns` → DNS servers

So `/etc/hosts` **overrides DNS**.

------

## 8. Common Use Cases

### 8.1 Access a Server by Name

Instead of:

```bash
ssh 192.168.1.10
```

Use:

```bash
ssh webserver
```

------

### 8.2 Local Testing

```text
127.0.0.1 mytest.com
```

Now:

```bash
ping mytest.com
```

resolves to `127.0.0.1`.

------

### 8.3 Block a Website (Simple Trick)

```text
127.0.0.1 facebook.com
```

The site will no longer load properly.

------

## 9. How to Edit `/etc/hosts`

You need **root privileges**.

### 9.1 Edit with Vim

```bash
sudo vi /etc/hosts
```

### 9.2 Backup First (Recommended)

```bash
sudo cp /etc/hosts /etc/hosts.bak
```

------

## 10. Do Changes Take Effect Immediately?

Yes ✅

No restart is needed.
Changes apply **immediately**.

Test with:

```bash
ping hostname
```

------

## 11. Common Beginner Mistakes

❌ Typing wrong IP address
❌ Forgetting to save the file
❌ Using tabs inconsistently (spaces are fine)
❌ Expecting `/etc/hosts` to work across multiple machines

Remember:

>   `/etc/hosts` works **only on the local machine**.

------

## 12. `/etc/hosts` vs DNS (Quick Comparison)

| Item         | /etc/hosts | DNS          |
| ------------ | ---------- | ------------ |
| Scope        | Local      | Network-wide |
| Easy to edit | Yes        | No           |
| Scalable     | No         | Yes          |
| Common usage | Testing    | Production   |

------

## 13. Security Note

-   `/etc/hosts` can be abused by malware
-   Always review it if network behavior looks strange

Check file permissions:

```bash
ls -l /etc/hosts
```

------

## 14. Summary

-   `/etc/hosts` maps IPs to names locally
-   Checked **before DNS**
-   Simple and powerful
-   Best for testing and small setups

If you understand `/etc/hosts`, you understand **basic hostname resolution** 👍