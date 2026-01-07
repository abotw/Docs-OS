# CentOS: ens33

Understanding `/etc/sysconfig/network-scripts/ifcfg-ens33`

## 1. What Is `ifcfg-ens33`?

In **CentOS 7**, network interfaces are configured using files located in:

```text
/etc/sysconfig/network-scripts/
```

Each network interface has **one configuration file**:

```text
ifcfg-<interface-name>
```

Example:

```text
ifcfg-ens33
```

This file controls:

-   IP address
-   DHCP or static IP
-   Gateway
-   DNS
-   Whether the network starts at boot

------

## 2. What Is `ens33`?

`ens33` is the **network interface name**.

Modern Linux uses **predictable network interface names**:

| Name    | Meaning                |
| ------- | ---------------------- |
| `ens33` | Ethernet + slot number |
| `eth0`  | Old-style naming       |
| `lo`    | Loopback interface     |

To list interfaces:

```bash
ip addr
```

------

## 3. When Is `ifcfg-ens33` Used?

`ifcfg-ens33` is used when:

-   CentOS boots
-   Network service restarts
-   Interface is brought up manually

The network service reads this file and configures the interface accordingly.

------

## 4. Typical `ifcfg-ens33` File Example

```ini
TYPE=Ethernet
BOOTPROTO=dhcp
NAME=ens33
DEVICE=ens33
ONBOOT=yes
```

This is a **DHCP-based configuration**.

------

## 5. Explanation of Common Fields

### 5.1 `TYPE`

```ini
TYPE=Ethernet
```

-   Network type
-   Usually `Ethernet`

------

### 5.2 `BOOTPROTO`

```ini
BOOTPROTO=dhcp
```

Controls how IP is obtained:

| Value    | Meaning              |
| -------- | -------------------- |
| `dhcp`   | Automatically get IP |
| `none`   | Static IP            |
| `static` | Same as `none`       |

------

### 5.3 `DEVICE`

```ini
DEVICE=ens33
```

-   Interface name
-   Must match the real interface name

------

### 5.4 `NAME`

```ini
NAME=ens33
```

-   Human-readable name
-   Usually same as `DEVICE`

------

### 5.5 `ONBOOT`

```ini
ONBOOT=yes
```

-   Whether the interface starts at boot
-   `yes` is recommended for servers

------

## 6. Static IP Configuration (Very Important)

Example of a **static IP** configuration:

```ini
TYPE=Ethernet
BOOTPROTO=none
NAME=ens33
DEVICE=ens33
ONBOOT=yes

IPADDR=192.168.1.100
PREFIX=24
GATEWAY=192.168.1.1
DNS1=8.8.8.8
DNS2=1.1.1.1
```

------

## 7. Explanation of Static IP Fields

### 7.1 `IPADDR`

```ini
IPADDR=192.168.1.100
```

-   The server’s IP address
-   Set this to your specific machine's IP

------

### 7.2 `PREFIX`

```ini
PREFIX=24
```

-   Subnet mask in CIDR format
-   `24` = `255.255.255.0`

------

### 7.3 `GATEWAY`

```ini
GATEWAY=192.168.1.1
```

-   Default gateway
-   Required for internet access

------

### 7.4 `DNS1`, `DNS2`

```ini
DNS1=8.8.8.8
DNS2=1.1.1.1
```

-   DNS servers
-   Used for domain name resolution

------

## 8. Restart Network After Editing

After editing the file, restart the network:

```bash
sudo systemctl restart network
```

Or bring the interface down and up:

```bash
sudo ifdown ens33
sudo ifup ens33
```

------

## 9. How to Edit the File Safely

Use a text editor:

```bash
sudo vi /etc/sysconfig/network-scripts/ifcfg-ens33
```

Before editing, make a backup:

```bash
sudo cp ifcfg-ens33 ifcfg-ens33.bak
```

------

## 10. Common Beginner Mistakes

❌ Interface name does not match
❌ `ONBOOT=no`
❌ Wrong gateway
❌ IP conflict on the network
❌ Forgetting to restart network

------

## 11. How to Check If It Works

### 11.1 Check IP

```bash
ip addr show ens33
```

### 11.2 Check Routing

```bash
ip route
```

### 11.3 Test Internet

```bash
ping 8.8.8.8
ping google.com
```

------

## 12. DHCP vs Static IP (Quick Comparison)

| Item               | DHCP      | Static |
| ------------------ | --------- | ------ |
| IP assignment      | Automatic | Manual |
| Easy to use        | Yes       | No     |
| Server recommended | No        | Yes    |
| Risk of IP change  | Yes       | No     |

------

## 13. Important Note (CentOS 8+)

In **CentOS 8 and later**:

-   `network-scripts` is deprecated
-   **NetworkManager** is used instead
-   Tools: `nmcli`, `nmtui`

But **CentOS 7 still widely uses `ifcfg-\*` files**.

------

## 14. Summary

-   `ifcfg-ens33` defines network settings for `ens33`
-   Located in `/etc/sysconfig/network-scripts/`
-   Controls DHCP, static IP, DNS, gateway
-   Changes require network restart

If you understand this file, you understand **basic Linux networking** 👍

