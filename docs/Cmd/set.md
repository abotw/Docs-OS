# set

The `set` command in Linux is a **built-in shell command** (works in Bash, Zsh, etc.) that can:

1.  **Display shell variables and functions**
2.  **Set shell options**
3.  **Control shell behavior**

It is a very powerful tool for shell scripting and debugging.

------

## 1. Basic Usage

### 1.1 View all shell variables and functions

```bash
set
```

-   Running `set` without arguments lists **all shell variables and functions** in the current shell.
-   Example:

```bash
$ set
BASH=/bin/bash
HOME=/home/user
PATH=/usr/local/bin:/usr/bin:/bin
...
my_function () {
    echo "Hello"
}
```

>   Tip: `set` lists variables **alphabetically**, unlike `env` or `printenv`, which only show **environment variables**.

------

### 1.2 Set a shell variable

```bash
set VARIABLE_NAME=value
```

-   Example:

```bash
set MY_VAR="Hello"
echo $MY_VAR
# Output: Hello
```

>   Note: In Bash, it’s more common to just use `MY_VAR="Hello"` without `set`. Using `set` is optional for simple variables.

------

## 2. `set` Options (Shell Behavior)

You can use `set` with **flags** to control how the shell behaves.

### 2.1 Enable debugging: `-x`

```bash
set -x
```

-   Prints each command before executing it.
-   Useful for **debugging scripts**.

```bash
#!/bin/bash
set -x
echo "Hello"
VAR=5
echo $VAR
```

**Output:**

```
+ echo 'Hello'
Hello
+ VAR=5
+ echo 5
5
```

### 2.2 Disable debugging: `+x`

```bash
set +x
```

------

### 2.3 Treat unset variables as errors: `-u`

```bash
set -u
echo $UNDEFINED_VAR
```

-   If `UNDEFINED_VAR` is not set, the shell will **exit with an error**.
-   Helps catch **typos and mistakes** in scripts.

### 2.4 Exit on error: `-e`

```bash
set -e
```

-   Makes the shell **exit immediately** if a command fails (returns non-zero).
-   Example:

```bash
set -e
ls /not_exist_dir
echo "This will not print"
```

### 2.5 Combine multiple options

```bash
set -eux
```

-   `-e` → exit on error
-   `-u` → treat unset variables as errors
-   `-x` → debug mode (print commands)
-   Useful for **robust scripting**.

------

## 3. Stop all options: `set +o`

```bash
set +o
```

-   Displays all shell options with **on/off** status.

### 3.1 Turn off a specific option

```bash
set +e  # stop exiting on error
set +u  # stop error on unset variable
```

### 3.2 Turn on a specific option

```bash
set -o errexit  # same as set -e
set -o nounset  # same as set -u
set -o xtrace   # same as set -x
```

------

## 4. Common Shell Options (for Beginners)

| Option      | Shortcut | Description                            |
| ----------- | -------- | -------------------------------------- |
| `errexit`   | `-e`     | Exit script if a command fails         |
| `nounset`   | `-u`     | Treat unset variables as errors        |
| `xtrace`    | `-x`     | Print each command before executing    |
| `noglob`    | `-f`     | Disable pathname expansion (wildcards) |
| `ignoreeof` | none     | Prevent `Ctrl+D` from exiting shell    |

------

## 5. Summary

-   `set` without arguments → show all shell variables/functions.
-   `set VARIABLE=value` → set a shell variable.
-   `set -x` → debug mode.
-   `set -e` → exit on error.
-   `set -u` → unset variables cause errors.
-   `set +o` → list shell options.

>   Tips for beginners:
>
>   -   Use `set -eux` in scripts to catch errors early.
>   -   Use `set +x` to stop debug output when not needed.
>   -   Remember: `set` changes only the **current shell session**, unless used in scripts.