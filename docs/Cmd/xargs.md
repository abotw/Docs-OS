# xargs

## 1. What is `xargs`?

`xargs` means **“extended arguments”**.

It is used to:

👉 **Take input from standard input (stdin) and turn it into command arguments**

In simple words:

>   `xargs` connects commands that output text
>   with commands that require arguments.

------

## 2. Why Do We Need `xargs`?

Many commands **output text**, but other commands **need arguments**.

Example problem:

```bash
find . -name "*.log" | rm
```

❌ This does not work because `rm` needs file names as arguments.

Solution:

```bash
find . -name "*.log" | xargs rm
```

✔ `xargs` passes the file names to `rm`.

------

## 3. Basic Syntax

```bash
command1 | xargs command2
```

Example:

```bash
echo "a b c" | xargs rm
```

Equivalent to:

```bash
rm a b c
```

------

## 4. Your First `xargs` Example

### Print Words on One Line

```bash
echo "hello world linux" | xargs
```

Output:

```text
hello world linux
```

------

### Convert Lines to Arguments

```bash
printf "a\nb\nc\n" | xargs echo
```

Output:

```text
a b c
```

------

## 5. Common `xargs` Use Cases

### 5.1 Remove Files

```bash
ls *.tmp | xargs rm
```

Better (safer):

```bash
ls *.tmp | xargs rm -v
```

------

### 5.2 Count Lines in Many Files

```bash
ls *.txt | xargs wc -l
```

------

### 5.3 Search Inside Files

```bash
grep -l error *.log | xargs less
```

------

## 6. Important Options (Beginner Must-Know)

| Option  | Meaning                          |
| ------- | -------------------------------- |
| `-n N`  | Use N arguments per command      |
| `-I {}` | Replace placeholder              |
| `-0`    | Input items are separated by NUL |
| `-p`    | Prompt before execution          |
| `-t`    | Print command before executing   |

## 7. Limit Arguments per Command (`-n`)

```bash
echo "1 2 3 4" | xargs -n 2 echo
```

Output:

```text
1 2
3 4
```

------

## 8. Use Placeholder (`-I {}`)

```bash
ls *.txt | xargs -I {} cp {} backup/
```

✔ `{}` represents each input item.

------

## 9. Handle Spaces in File Names (Very Important!)

### ❌ Problem

```bash
ls | xargs rm
```

Fails for:

```text
my file.txt
```

------

### ✅ Correct Way (`-print0` + `-0`)

```bash
find . -name "*.tmp" -print0 | xargs -0 rm
```

This is **the safest way**.

------

## 10. Ask Before Executing (`-p`)

```bash
ls *.log | xargs -p rm
```

You will be asked for confirmation.

------

## 11. Show Commands Before Running (`-t`)

```bash
ls *.log | xargs -t rm
```

Output:

```text
rm a.log b.log
```

------

## 12. `xargs` vs Loop

### Using a Loop

```bash
for f in *.txt; do
    wc -l "$f"
done
```

### Using `xargs`

```bash
ls *.txt | xargs wc -l
```

✔ Shorter and often faster.

------

## 13. When NOT to Use `xargs`

-   When the command already supports multiple files directly
-   When filenames may contain newlines (unless using `-0`)
-   When clarity is more important than brevity

------

## 14. Practical Examples

### Kill Processes by Name

```bash
ps aux | grep nginx | awk '{print $2}' | xargs kill
```

(Safer alternative exists, but this shows the idea.)

------

### Change Permissions

```bash
find . -type f -name "*.sh" | xargs chmod +x
```

------

### Compress Many Files

```bash
ls *.log | xargs tar -czvf logs.tar.gz
```

------

## 15. Common Beginner Mistakes ⚠️

### ❌ Forgetting File Safety

```bash
ls | xargs rm
```

### ✅ Safer

```bash
find . -type f -print0 | xargs -0 rm
```

------

### ❌ Using `xargs` When Not Needed

```bash
rm $(ls *.tmp)
```

This may break for many files.

------

## 16. Quick Cheat Sheet

```bash
cmd | xargs cmd2
xargs -n 1 cmd
xargs -I {} cmd {}
xargs -0 cmd
xargs -p cmd
```

------

## 17. Summary

-   `xargs` converts stdin into command arguments
-   Very powerful with pipes
-   Be careful with spaces and special characters
-   Use `-print0` and `-0` for safety