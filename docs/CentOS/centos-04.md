# profile.d

## 1. What Is `/etc/profile.d/`?

`/etc/profile.d/` is a **directory** that contains **shell scripts**.

These scripts are:

-   Automatically executed **when a user logs in**
-   Applied **system-wide** (for all users)
-   Used to set **environment variables**, **PATH**, **aliases**, etc.

📌 In CentOS (and RHEL-based systems), `/etc/profile.d/` is sourced by `/etc/profile`.

## 2. When Are Scripts in `/etc/profile.d/` Executed?

For **login shells**, the execution order is roughly:

1.  `/etc/profile`
2.  All `*.sh` scripts in `/etc/profile.d/`
3.  User’s `~/.bash_profile` (or `~/.bash_login`, `~/.profile`)

So:

>   `/etc/profile.d/*.sh` runs **before user-specific config**

------

## 3. Why `/etc/profile.d/` Exists

Without `/etc/profile.d/`, all system-wide settings would have to be placed in one file:

```bash
/etc/profile
```

That would be messy.

Instead:

-   Each application adds its **own script**
-   Configuration is **modular and clean**

Examples:

-   `java.sh`
-   `maven.sh`
-   `go.sh`

------

## 4. What Kind of Files Go in `/etc/profile.d/`?

### ✔ Allowed

-   Shell scripts (`.sh`)
-   Environment variable definitions
-   PATH updates
-   Aliases and functions

### ❌ Not Recommended

-   Heavy logic
-   Long-running commands
-   Interactive commands (`read`, `vim`, `echo` spam)

------

## 5. File Naming Rules

-   Must end with `.sh`
-   Must be readable
-   Usually owned by `root`

Example:

```text
/etc/profile.d/java.sh
```

------

## 6. Simple Example: Add JAVA_HOME

### 6.1 Create Script (Root Required)

```bash
sudo vim /etc/profile.d/java.sh
export JAVA_HOME=/usr/lib/jvm/java-17
export PATH=$JAVA_HOME/bin:$PATH
```

------

### 6.2 Apply Changes

Log out and log in again, or:

```bash
source /etc/profile
```

Check:

```bash
echo $JAVA_HOME
java -version
```

------

## 7. Example: Add a Custom PATH

```bash
sudo vim /etc/profile.d/tools.sh
export PATH=/opt/tools/bin:$PATH
```

------

## 8. Example: Define Aliases

```bash
sudo vim /etc/profile.d/aliases.sh
alias ll='ls -lh'
alias gs='git status'
```

After login:

```bash
ll
gs
```

------

## 9. Which Shells Use `/etc/profile.d/`?

| Shell  | Supported         |
| ------ | ----------------- |
| `bash` | ✅ Yes             |
| `sh`   | ✅ Yes             |
| `zsh`  | ❌ No (by default) |
| `fish` | ❌ No              |

📌 `/etc/profile.d/` works **only for shells that read `/etc/profile`**.

------

## 10. Login Shell vs Non-Login Shell

### Login Shell (Works)

```bash
ssh user@host
su - user
```

------

### Non-Login Shell (Does NOT run `/etc/profile.d/`)

```bash
bash
```

To apply settings:

```bash
source /etc/profile
```

------

## 11. `/etc/profile.d/` vs Other Config Files

| File                  | Scope                   |
| --------------------- | ----------------------- |
| `/etc/profile`        | System-wide, login      |
| `/etc/profile.d/*.sh` | System-wide, modular    |
| `~/.bash_profile`     | User login              |
| `~/.bashrc`           | Interactive shell       |
| `/etc/bashrc`         | System-wide interactive |

------

## 12. Common Beginner Mistakes ⚠️

### ❌ Forgetting `.sh` Extension

```text
java
```

Script won’t be loaded.

------

### ❌ Using `echo` or `read`

```bash
echo "Welcome"
read name
```

Breaks login experience.

------

### ❌ Overwriting PATH

```bash
export PATH=/my/bin
```

### ✅ Correct

```bash
export PATH=/my/bin:$PATH
```

------

## 13. Debugging Tips

### Check Which Scripts Are Loaded

```bash
ls /etc/profile.d/
```

------

### Manually Test Script

```bash
source /etc/profile.d/java.sh
```

------

### Check Login Shell

```bash
echo $0
```

------

## 14. Practical Use Cases

-   System-wide Java / Maven / Go setup
-   Company-wide environment variables
-   Teaching lab environments
-   Shared servers

------

## 15. Summary

-   `/etc/profile.d/` stores **system-wide login shell scripts**
-   Files must end with `.sh`
-   Executed for **all users**
-   Best place for global environment variables
-   Cleaner than editing `/etc/profile` directly