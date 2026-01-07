# tar

## 1. What is `tar`?

`tar` stands for **Tape Archive**.
It is a classic Linux/Unix command used to:

-   **Pack multiple files/directories into one file** (archive)
-   **Extract files from an archive**
-   Often used together with compression tools like **gzip**, **bzip2**, or **xz**

Common file extensions:

-   `.tar` → archive only
-   `.tar.gz` or `.tgz` → tar + gzip
-   `.tar.bz2` → tar + bzip2
-   `.tar.xz` → tar + xz

------

## 2. Basic Syntax

```bash
tar [options] archive_name files_or_directories
```

Example:

```bash
tar -cf archive.tar file1 file2 dir1
```

------

## 3. Most Important Options (Must Know)

| Option   | Meaning                       |
| -------- | ----------------------------- |
| `-c`     | Create an archive             |
| **`-x`** | **Extract an archive**        |
| `-t`     | List contents of an archive   |
| **`-f`** | **Specify archive file name** |
| **`-v`** | **Verbose (show progress)**   |
| **`-z`** | **Use gzip compression**      |
| `-j`     | Use bzip2 compression         |
| `-J`     | Use xz compression            |
| `-C`     | Extract to a directory        |

>   ⚠️ **Important:**
>   `-f` must be **followed immediately by the archive name**

------

## 4. Creating a `.tar` Archive

### 4.1 Archive a Single File

```bash
tar -cf file.tar file.txt
```

------

### 4.2 Archive Multiple Files

```bash
tar -cf files.tar a.txt b.txt c.txt
```

------

### 4.3 Archive a Directory

```bash
tar -cf project.tar project/
```

>   This includes all subdirectories and files.

------

### 4.4 Show Progress While Creating (`-v`)

```bash
tar -cvf project.tar project/
```

------

## 5. Extracting Archives

### 5.1 Extract a `.tar` File

```bash
tar -xf project.tar
```

------

### 5.2 Extract with Verbose Output

```bash
tar -xvf project.tar
```

------

### 5.3 Extract to a Specific Directory

```bash
tar -xf project.tar -C /tmp
```

>   The directory must already exist.

------

## 6. Listing Archive Contents (Without Extracting)

```bash
tar -tf project.tar
```

With details:

```bash
tar -tvf project.tar
```

------

## 7. Using Compression

### 7.1 Create a `.tar.gz` (Most Common)

```bash
tar -czvf project.tar.gz project/
```

Breakdown:

-   `-c` create
-   `-z` gzip
-   `-v` verbose
-   `-f` file

------

### 7.2 Extract a `.tar.gz`

```bash
tar -xzvf project.tar.gz
```

------

### 7.3 Create a `.tar.bz2`

```bash
tar -cjvf project.tar.bz2 project/
```

Extract:

```bash
tar -xjvf project.tar.bz2
```

------

### 7.4 Create a `.tar.xz` (Best Compression)

```bash
tar -cJvf project.tar.xz project/
```

Extract:

```bash
tar -xJvf project.tar.xz
```

------

## 8. Common Beginner Mistakes ⚠️

### ❌ Forgetting `-f`

```bash
tar -cv project.tar project/   # WRONG
```

### ✅ Correct

```bash
tar -cvf project.tar project/
```

------

### ❌ Wrong Order (Archive name not after `-f`)

```bash
tar -cf project/ project.tar   # WRONG
```

### ✅ Correct

```bash
tar -cf project.tar project/
```

------

## 9. Practical Examples

### Backup `/etc` Directory

```bash
tar -czvf etc-backup.tar.gz /etc
```

------

### Extract Only One File from Archive

```bash
tar -xvf project.tar README.md
```

------

### Check Archive Before Extracting

```bash
tar -tf project.tar
```

------

## 10. Quick Reference Cheat Sheet

```bash
# Create tar
tar -cf archive.tar dir/

# Extract tar
tar -xf archive.tar

# Create tar.gz
tar -czvf archive.tar.gz dir/

# Extract tar.gz
tar -xzvf archive.tar.gz

# List contents
tar -tf archive.tar
```

------

## 11. Summary

-   `tar` is for **archiving**, not compression (compression is optional)
-   `-c` create, `-x` extract, `-t` list
-   `-f` is mandatory
-   Compression options: `-z`, `-j`, `-J`
-   Widely used for backups, source code, and software distribution