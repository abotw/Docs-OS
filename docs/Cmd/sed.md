# sed

## 1. What is `sed`?

`sed` stands for **Stream Editor**.
It is a **non-interactive text processing tool** used to:

-   Search and replace text
-   Insert, delete, or modify lines
-   Transform text in pipelines
-   Process large files efficiently

`sed` works **line by line**, reading input from:

-   Files
-   Standard input (pipes)

It **does not modify files by default** — it prints results to standard output.

------

## 2. Basic Syntax

```bash
sed 'command' file
```

or with pipes:

```bash
command | sed 'command'
```

Example:

```bash
sed 'p' file.txt
```

------

## 3. How `sed` Works (Core Idea)

For each line:

1.  Read one line into **pattern space**
2.  Apply the command(s)
3.  Print the result (unless suppressed)
4.  Move to the next line

------

## 4. Printing Lines

### 4.1 Print Every Line (Default)

```bash
sed '' file.txt
```

Same as:

```bash
cat file.txt
```

------

### 4.2 Print Specific Lines

Use `-n` to suppress automatic output.

```bash
sed -n 'p' file.txt
```

Print line **3**:

```bash
sed -n '3p' file.txt
```

Print lines **3 to 5**:

```bash
sed -n '3,5p' file.txt
```

Print the **last line**:

```bash
sed -n '$p' file.txt
```

------

## 5. Deleting Lines

Delete line **3**:

```bash
sed '3d' file.txt
```

Delete lines **3–5**:

```bash
sed '3,5d' file.txt
```

Delete empty lines:

```bash
sed '/^$/d' file.txt
```

------

## 6. Search and Replace (MOST IMPORTANT)

### 6.1 Basic Substitution

```bash
sed 's/old/new/' file.txt
```

-   Replaces **first match per line**

Example:

```bash
sed 's/apple/orange/' file.txt
```

------

### 6.2 Global Replacement

```bash
sed 's/old/new/g' file.txt
```

Replace all matches in each line.

------

### 6.3 Replace on Specific Lines

Only on line 3:

```bash
sed '3s/old/new/' file.txt
```

Only on lines 3–5:

```bash
sed '3,5s/old/new/g' file.txt
```

------

### 6.4 Replace Lines Matching a Pattern

```bash
sed '/ERROR/s/old/new/' file.txt
```

------

## 7. Using Regular Expressions

### 7.1 Common Regex Symbols

| Symbol | Meaning       |
| ------ | ------------- |
| `^`    | Line start    |
| `$`    | Line end      |
| `.`    | Any character |
| `*`    | Zero or more  |
| `.*`   | Anything      |
| `[]`   | Character set |

Example: Replace numbers

```bash
sed 's/[0-9]/X/g' file.txt
```

------

### 7.2 Anchors

Replace lines starting with `root`:

```bash
sed 's/^root/USER/' file.txt
```

Replace lines ending with `.log`:

```bash
sed 's/\.log$/\.bak/' file.txt
```

------

## 8. Inserting and Appending Text

### 8.1 Insert Before a Line

```bash
sed '3i\NEW LINE' file.txt
```

------

### 8.2 Append After a Line

```bash
sed '3a\NEW LINE' file.txt
```

------

### 8.3 Change a Line

```bash
sed '3c\THIS LINE IS REPLACED' file.txt
```

## 9. Working with Files (In-Place Editing)

⚠️ **Be careful** — this modifies the file.

```bash
sed -i 's/old/new/g' file.txt
```

On macOS (BSD sed):

```bash
sed -i '' 's/old/new/g' file.txt
```

Create a backup:

```bash
sed -i.bak 's/old/new/g' file.txt
```

------

## 10. Multiple Commands

### 10.1 Using `;`

```bash
sed 's/foo/bar/g; s/hello/hi/g' file.txt
```

------

### 10.2 Using `-e`

```bash
sed -e 's/foo/bar/g' -e 's/hello/hi/g' file.txt
```

------

## 11. Using `sed` with Pipes

Replace spaces with commas:

```bash
ls | sed 's/ /,/g'
```

Filter and transform:

```bash
ps aux | sed -n '1,5p'
```

------

## 12. Practical Examples

### Remove comments

```bash
sed 's/#.*//' file.conf
```

------

### Trim leading spaces

```bash
sed 's/^[ \t]*//' file.txt
```

------

### Trim trailing spaces

```bash
sed 's/[ \t]*$//' file.txt
```

------

### Number lines

```bash
sed = file.txt | sed 'N; s/\n/\t/'
```

## 13. GNU sed vs BSD sed (Important!)

| Feature | GNU sed (Linux) | BSD sed (macOS)  |
| ------- | --------------- | ---------------- |
| `-i`    | `sed -i`        | `sed -i ''`      |
| Regex   | More features   | Slightly limited |

Always test commands before using `-i`.

------

## 14. When to Use `sed`

Use `sed` when:

-   You need fast, scriptable text processing
-   You work with pipelines
-   You modify large files

Avoid `sed` when:

-   You need complex logic → use `awk` or Python

------

## 15. Summary

-   `sed` is a **powerful stream editor**
-   Best for **search/replace**, **line editing**, **pipelines**
-   Learn these first:
    -   `s///`
    -   `p`, `d`
    -   `-n`
    -   regex basics