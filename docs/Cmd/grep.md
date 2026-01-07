# grep

## 1. What is `grep`?

`grep` stands for **Global Regular Expression Print**.

It is used to:

-   **Search text for specific patterns**
-   Print lines that **match** a keyword or pattern
-   Work with files, directories, and command output

`grep` is one of the most important and frequently used Linux commands.

------

## 2. Basic Syntax

```bash
grep [options] PATTERN FILE
```

Examples:

```bash
grep root /etc/passwd
grep error logfile.txt
```

------

## 3. Your First `grep`

### Search for a Word in a File

```bash
grep linux notes.txt
```

✔ Prints all lines in `notes.txt` that contain `linux`.

------

### Case Sensitivity

By default, `grep` **is case-sensitive**:

```bash
grep Linux notes.txt
```

------

### Ignore Case (`-i`)

```bash
grep -i linux notes.txt
```

Matches:

-   linux
-   Linux
-   LINUX

## 4. Searching Multiple Files

```bash
grep main *.c
```

Shows matching lines and file names.

------

## 5. Commonly Used Options (Beginner Must-Know)

| Option         | Meaning                     |
| -------------- | --------------------------- |
| `-i`           | Ignore case                 |
| `-n`           | Show line numbers           |
| `-v`           | Invert match (NOT matching) |
| `-r` / `-R`    | Recursive search            |
| `-l`           | Show only file names        |
| `-c`           | Count matching lines        |
| `-w`           | Match whole word            |
| `--color=auto` | Highlight matches           |

------

## 6. Show Line Numbers (`-n`)

```bash
grep -n error app.log
```

Output:

```text
15:error: connection failed
```

------

## 7. Search for Lines That Do NOT Match (`-v`)

```bash
grep -v root /etc/passwd
```

✔ Shows all users except `root`.

------

## 8. Recursive Search in Directories (`-r`)

```bash
grep -r TODO .
```

Searches all files under the current directory.

------

## 9. Search Only File Names (`-l`)

```bash
grep -l main *.c
```

Output:

```text
main.c
test.c
```

------

## 10. Count Matches (`-c`)

```bash
grep -c error app.log
```

Counts matching **lines**, not occurrences.

------

## 11. Match Whole Words (`-w`)

```bash
grep -w cat animals.txt
```

✔ Matches `cat`
❌ Does not match `catch`, `category`

------

## 12. Use `grep` with Pipes (`|`)

Very common usage:

```bash
ps aux | grep nginx
dmesg | grep -i usb
ls -l | grep '^d'
```

------

## 13. Basic Regular Expressions (Beginner Level)

### 13.1 Beginning of Line (`^`)

```bash
grep '^root' /etc/passwd
```

------

### 13.2 End of Line (`$`)

```bash
grep 'bash$' /etc/passwd
```

------

### 13.3 Match Any Character (`.`)

```bash
grep 'h.t' file.txt
```

Matches:

-   hat
-   hit
-   hot

------

### 13.4 Character Classes

```bash
grep '[0-9]' file.txt
```

Matches lines containing digits.

------

## 14. `grep` Variants

| Command | Purpose                            |
| ------- | ---------------------------------- |
| `grep`  | Basic search                       |
| `egrep` | Extended regex (same as `grep -E`) |
| `fgrep` | Fixed strings (same as `grep -F`)  |

Examples:

```bash
grep -E 'error|fail' app.log
grep -F 'a+b' file.txt
```

------

## 15. Common Beginner Mistakes ⚠️

### ❌ Forgetting Quotes

```bash
grep error|fail file.txt
```

Shell interprets `|`.

### ✅ Correct

```bash
grep 'error|fail' file.txt
```

------

### ❌ Searching Binary Files

```bash
grep text program
```

May produce garbage output.

### ✅ Better

```bash
grep -I text program
```

------

## 16. Practical Examples

### Find Failed SSH Logins

```bash
grep "Failed password" /var/log/secure
```

------

### Search Configuration Files

```bash
grep -r "Listen" /etc/httpd
```

------

### Find TODO Comments in Code

```bash
grep -rn TODO .
```

------

## 17. Quick Cheat Sheet

```bash
grep word file
grep -i word file
grep -n word file
grep -v word file
grep -r word dir
grep -E 'a|b' file
```

------

## 18. Summary

-   `grep` searches text using patterns
-   Extremely powerful when combined with pipes
-   Start with simple keywords, then learn regex
-   Essential for logs, configs, and debugging