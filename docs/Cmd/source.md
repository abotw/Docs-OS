# source

## 1. What is `source`?

`source` is a **shell built-in command** used to:

👉 **Read and execute commands from a file in the current shell environment**

This is very important:

>   **Commands run by `source` affect your current shell**,
>   unlike running a script normally, which starts a new shell.

## 2. Basic Syntax

```bash
source filename
```

or the shorter form:

```bash
. filename
```

Both are **exactly the same**.

## 3. Why `source` Is Important

Normally, when you run a script:

```bash
./script.sh
```

-   It runs in a **subshell**
-   Environment changes (variables, `cd`, `export`) **do not affect your current shell**

But with `source`:

```bash
source script.sh
```

-   It runs in the **current shell**
-   Changes **remain after execution**

------

## 4. Simple Example

### 4.1 Create a Script

```bash
vim test.sh
#!/bin/bash
MYVAR="hello"
export MYVAR
```

------

### 4.2 Run Normally (Subshell)

```bash
./test.sh
echo $MYVAR
```

Output:

```text
(empty)
```

------

### 4.3 Run with `source`

```bash
source test.sh
echo $MYVAR
```

Output:

```text
hello
```

✔ The variable exists because it was set in the current shell.

------

## 5. `source` vs `./script.sh`

| Method             | Runs in       | Environment Changed? |
| ------------------ | ------------- | -------------------- |
| `./script.sh`      | Subshell      | ❌ No                 |
| `bash script.sh`   | Subshell      | ❌ No                 |
| `source script.sh` | Current shell | ✅ Yes                |
| `. script.sh`      | Current shell | ✅ Yes                |

------

## 6. Common Use Cases

### 6.1 Reload Shell Configuration

After editing `.bashrc`:

```bash
vim ~/.bashrc
```

Apply changes immediately:

```bash
source ~/.bashrc
```

Without this, you would need to open a new terminal.

------

### 6.2 Load Environment Variables

File: `env.sh`

```bash
export JAVA_HOME=/usr/lib/jvm/java-17
export PATH=$JAVA_HOME/bin:$PATH
```

Load it:

```bash
source env.sh
```

------

### 6.3 Activate Python Virtual Environment

```bash
source venv/bin/activate
```

This works **only** with `source`, not `./activate`.

------

### 6.4 Define Functions and Aliases

```bash
# tools.sh
myll() {
    ls -lh
}

alias gs='git status'
```

Load them:

```bash
source tools.sh
```

------

## 7. The `.` (Dot) Command

This is the POSIX-compatible form:

```bash
. filename
```

Example:

```bash
. ~/.bash_profile
```

✔ Works in `sh`, `bash`, and other shells.

------

## 8. Common Beginner Mistakes ⚠️

### ❌ Forgetting File Path

```bash
source test.sh
```

If the file is in the current directory, this may fail.

### ✅ Correct

```bash
source ./test.sh
```

------

### ❌ Expecting `cd` to Persist Without `source`

```bash
./change_dir.sh
pwd   # directory unchanged
```

### ✅ Correct

```bash
source change_dir.sh
pwd   # directory changed
```

------

### ❌ Sourcing Untrusted Scripts

```bash
source unknown.sh
```

⚠️ This can be **dangerous**, because it runs **with your current shell permissions**.

------

## 9. When NOT to Use `source`

-   Running long automation scripts
-   Running untrusted scripts
-   Scripts that should not affect your environment

Use normal execution instead:

```bash
./script.sh
```

------

## 10. Practical Example: Config File Pattern

```bash
# config.sh
DB_HOST=localhost
DB_PORT=3306
```

Main script:

```bash
source config.sh
echo "$DB_HOST:$DB_PORT"
```

------

## 11. Summary

-   `source` executes a file **in the current shell**
-   Changes to variables, functions, aliases **persist**
-   `. filename` is equivalent to `source filename`
-   Commonly used for:
    -   Shell config files
    -   Environment variables
    -   Virtual environment activation