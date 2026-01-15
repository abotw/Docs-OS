# awk

## 1. What is `awk`?

`awk` is a **text processing and reporting tool** designed to work with:

-   Structured text
-   Columns (fields)
-   Line-based records

It is especially good for:

-   Processing tables
-   Log analysis
-   Data extraction
-   Simple calculations

If:

-   `sed` = *line editor*
-   `awk` = *mini programming language for text*

------

## 2. When Should You Use `awk`?

Use `awk` when:

-   Data is **column-based**
-   You need **conditions**
-   You need **calculations or statistics**
-   You need **formatted output**

Example input:

```text
Tom  18  85
Bob  20  90
Lucy 19  88
```

------

## 3. Basic Syntax

```bash
awk 'pattern { action }' file
```

-   `pattern` → condition (optional)
-   `action` → what to do (usually print)

If `pattern` is omitted → applies to all lines
If `action` is omitted → default is `{ print }`

------

## 4. Your First `awk` Command

Print entire file:

```bash
awk '{ print }' file.txt
```

Same as:

```bash
cat file.txt
```

------

## 5. Fields and Records (CORE CONCEPT)

-   Each **line** = one **record**
-   Each **column** = one **field**

Default field separator: **spaces or tabs**

| Variable | Meaning          |
| -------- | ---------------- |
| `$0`     | Entire line      |
| `$1`     | First field      |
| `$2`     | Second field     |
| `NF`     | Number of fields |
| `NR`     | Line number      |

Example:

```bash
awk '{ print $1, $3 }' file.txt
```

------

## 6. Printing Selected Fields

Print name and score:

```bash
awk '{ print $1, $3 }' scores.txt
```

Print last field:

```bash
awk '{ print $NF }' file.txt
```

------

## 7. Using Conditions (Patterns)

Print lines where score > 85:

```bash
awk '$3 > 85 { print $1, $3 }' scores.txt
```

Print lines containing "ERROR":

```bash
awk '/ERROR/ { print }' log.txt
```

------

## 8. Built-in Variables

| Variable | Description             |
| -------- | ----------------------- |
| `NR`     | Record number           |
| `NF`     | Field count             |
| `FS`     | Field separator         |
| `OFS`    | Output field separator  |
| `RS`     | Record separator        |
| `ORS`    | Output record separator |

Print line number + content:

```bash
awk '{ print NR, $0 }' file.txt
```

------

## 9. Changing Field Separators

### 9.1 Using `-F`

Comma-separated file:

```bash
awk -F ',' '{ print $1, $2 }' data.csv
```

Colon-separated:

```bash
awk -F ':' '{ print $1 }' /etc/passwd
```

------

### 9.2 Inside awk

```bash
awk 'BEGIN { FS=":" } { print $1 }' /etc/passwd
```

------

## 10. BEGIN and END Blocks

### 10.1 BEGIN

Executed **before reading input**

```bash
awk 'BEGIN { print "Start processing" } { print $1 }' file.txt
```

------

### 10.2 END

Executed **after all lines**

```bash
awk '{ sum += $3 } END { print "Total:", sum }' scores.txt
```

------

## 11. Simple Calculations

Average score:

```bash
awk '{ sum += $3 } END { print sum/NR }' scores.txt
```

------

## 12. String Functions

| Function    | Description   |
| ----------- | ------------- |
| `length()`  | String length |
| `tolower()` | Lowercase     |
| `toupper()` | Uppercase     |
| `substr()`  | Substring     |
| `index()`   | Find position |

Example:

```bash
awk '{ print toupper($1) }' file.txt
```

------

## 13. Conditions (if / else)

```bash
awk '{
  if ($3 >= 90)
    print $1, "Excellent"
  else
    print $1, "OK"
}' scores.txt
```

------

## 14. Loops

### for loop

```bash
awk '{
  for (i=1; i<=NF; i++)
    print $i
}' file.txt
```

------

## 15. Formatting Output

```bash
awk '{ printf "%-10s %5d\n", $1, $3 }' scores.txt
```

-   `printf` does **not** add newline automatically

------

## 16. Using `awk` with Pipes

```bash
ps aux | awk '{ print $1, $2 }'
ls -l | awk '{ print $9, $5 }'
```

------

## 17. Practical Examples

### Sum file sizes

```bash
ls -l | awk '{ sum += $5 } END { print sum }'
```

------

### Count lines

```bash
awk 'END { print NR }' file.txt
```

------

### Remove duplicate lines

```bash
awk '!seen[$0]++' file.txt
```

------

### Extract IP addresses

```bash
awk '{ print $1 }' access.log
```

------

## 18. `awk` vs `sed`

| Feature         | sed  | awk     |
| --------------- | ---- | ------- |
| Line editing    | Yes  | Limited |
| Column handling | No   | Yes     |
| Calculations    | No   | Yes     |
| Programming     | No   | Yes     |

------

## 19. Common awk Versions

-   `awk` → system default
-   `gawk` → GNU awk (most common on Linux)
-   `mawk` → faster, lightweight

Check version:

```bash
awk --version
```

------

## 20. Summary

-   `awk` is **perfect for structured text**
-   Think in terms of:
    -   records (lines)
    -   fields (columns)
-   Learn first:
    -   `$1`, `$2`, `$NF`
    -   `NR`, `NF`
    -   `BEGIN`, `END`
    -   conditions