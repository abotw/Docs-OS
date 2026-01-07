# wget

## 1. What is `wget`?

`wget` is a **command-line tool** used to **download files from the internet**.
It supports HTTP, HTTPS, and FTP protocols and works well even on unstable networks.

Typical use cases:

-   Download software packages
-   Fetch files from a server
-   Download files in the background
-   Mirror a website

------

## 2. Check if `wget` is installed

Most Linux distributions come with `wget` preinstalled.

```bash
wget --version
```

If not installed:

### Ubuntu / Debian

```bash
sudo apt update
sudo apt install wget
```

### CentOS / Rocky / AlmaLinux

```bash
sudo yum install wget
```

------

## 3. Basic usage

### Download a file

```bash
wget https://example.com/file.zip
```

The file will be saved in the **current directory**.

------

### Specify output filename

```bash
wget -O myfile.zip https://example.com/file.zip
```

------

### Download to a specific directory

```bash
wget -P /tmp https://example.com/file.zip
```

------

## 4. Download in the background

Useful for large files or remote servers.

```bash
wget -b https://example.com/large.iso
```

Check progress:

```bash
tail -f wget-log
```

------

## 5. Resume an interrupted download

If a download stops due to network issues:

```bash
wget -c https://example.com/large.iso
```

(`-c` means **continue**)

------

## 6. Download multiple files

### From a list file

Create a file:

```bash
vim urls.txt
```

Example content:

```
https://example.com/a.zip
https://example.com/b.zip
https://example.com/c.zip
```

Download all:

```bash
wget -i urls.txt
```

------

## 7. Limit download speed

Useful to avoid consuming all bandwidth.

```bash
wget --limit-rate=500k https://example.com/file.iso
```

------

## 8. Download with authentication

### HTTP username & password

```bash
wget --user=username --password=password https://example.com/file
```

⚠️ Passwords may appear in shell history.

------

## 9. Download an entire website (basic)

```bash
wget -r https://example.com
```

Common options:

-   `-r` → recursive
-   `-np` → no parent directory
-   `-k` → convert links for local use
-   `-p` → download page assets (CSS, images)

Example:

```bash
wget -r -np -k -p https://example.com
```

------

## 10. Common options summary

| Option         | Meaning             |
| -------------- | ------------------- |
| `-O`           | Output filename     |
| `-P`           | Output directory    |
| `-c`           | Resume download     |
| `-b`           | Background download |
| `-i`           | Read URLs from file |
| `-r`           | Recursive download  |
| `--limit-rate` | Limit speed         |

------

## 11. When to use `wget` vs `curl`

| `wget`                       | `curl`                   |
| ---------------------------- | ------------------------ |
| Best for downloading files   | Best for APIs & requests |
| Supports recursive downloads | No recursion             |
| Simple and robust            | More flexible            |

👉 **Rule of thumb**:
Use **`wget`** for downloading files, **`curl`** for interacting with APIs.

------

## 12. Practice examples

```bash
wget https://example.com/test.txt
wget -c https://example.com/large.iso
wget -P ~/Downloads https://example.com/app.tar.gz
```

------

## 13. Get help

```bash
wget --help
man wget
```

------

## ✅ Summary

-   `wget` is a powerful and simple download tool
-   Ideal for servers, scripts, and automation
-   Works well over slow or unstable networks