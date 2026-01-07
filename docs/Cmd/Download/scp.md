# scp

## 1. What is `scp`?

`scp` stands for **Secure Copy**.

It is used to:

-   **Copy files and directories between computers**
-   Work over **SSH**
-   Encrypt data during transfer

📌 If you can `ssh` to a machine, you can use `scp`.

------

## 2. Basic Syntax

```bash
scp [options] source destination
```

At least **one side must be remote**.

------

## 3. Copy a File from Local to Remote

```bash
scp file.txt user@remote:/home/user/
```

Example:

```bash
scp notes.txt mql@192.168.1.100:/home/mql/
```

------

## 4. Copy a File from Remote to Local

```bash
scp user@remote:/home/user/file.txt .
```

------

## 5. Copy Directories (`-r`)

```bash
scp -r project/ user@remote:/home/user/
```

Copy from remote:

```bash
scp -r user@remote:/home/user/project/ .
```

------

## 6. Commonly Used Options (Beginner Must-Know)

| Option | Meaning                          |
| ------ | -------------------------------- |
| `-r`   | Copy directories **r**ecursively |
| `-P`   | SSH port (uppercase)             |
| `-v`   | Verbose output                   |
| `-C`   | Enable compression               |
| `-p`   | Preserve timestamps and mode     |
| `-i`   | Specify SSH key                  |

------

## 7. Specify SSH Port (`-P`)

```bash
scp -P 2222 file.txt user@remote:/home/user/
```

⚠️ `-P` is uppercase.

------

## 8. Use SSH Key Authentication (`-i`)

```bash
scp -i ~/.ssh/id_ed25519 file.txt user@remote:/home/user/
```

------

## 9. Copy Multiple Files

```bash
scp a.txt b.txt user@remote:/home/user/
```

------

## 10. Show Progress and Details

```bash
scp -v bigfile.iso user@remote:/data/
```

------

## 11. Preserve File Attributes (`-p`)

```bash
scp -p config.conf user@remote:/etc/
```

Preserves:

-   Modification time
-   Permissions

------

## 12. Use Compression (`-C`)

```bash
scp -C bigfile user@remote:/backup/
```

Useful for slow networks.

------

## 13. Typical Beginner Scenarios

### Upload a File to a Server

```bash
scp app.tar.gz user@server:/opt/apps/
```

------

### Download Log Files

```bash
scp user@server:/var/log/messages .
```

------

### Copy Between Two Remote Servers

```bash
scp user1@host1:/data/file user2@host2:/backup/
```

(Your machine acts as a relay.)

------

## 14. Common Beginner Mistakes ⚠️

### ❌ Forgetting `-r` for Directories

```bash
scp folder user@remote:/tmp
```

### ✅ Correct

```bash
scp -r folder user@remote:/tmp
```

------

### ❌ Confusing `-p` and `-P`

```bash
scp -p 2222 file.txt ...
```

❌ Wrong.

### ✅ Correct

```bash
scp -P 2222 file.txt ...
```

------

### ❌ Wrong Path

```bash
scp file.txt user@remote:home/user
```

### ✅ Correct

```bash
scp file.txt user@remote:/home/user/
```

------

## 15. Security Tips

-   Always verify the SSH host fingerprint
-   Use SSH keys instead of passwords
-   Avoid copying files as `root` unless necessary

------

## 16. `scp` vs `rsync`

| Feature          | scp  | rsync |
| ---------------- | ---- | ----- |
| Simple           | ✅    | ❌     |
| Resume transfer  | ❌    | ✅     |
| Sync directories | ❌    | ✅     |
| Encrypted        | ✅    | ✅     |

📌 Use `scp` for **simple copy**, `rsync` for **sync/backup**.

------

## 17. Quick Cheat Sheet

```bash
scp file user@host:/path
scp user@host:/path/file .
scp -r dir user@host:/path
scp -P 22 file user@host:/path
scp -i key file user@host:/path
```

------

## 18. Summary

-   `scp` copies files securely over SSH
-   Easy to use for quick transfers
-   Supports files and directories
-   Depends on SSH configuration