# OpenWrt-01: Intro

## 1. What Is OpenWrt?

**OpenWrt** is an **open-source embedded Linux operating system** designed mainly for **routers and network devices**.

Unlike stock router firmware (from TP-Link, Xiaomi, ASUS, etc.), OpenWrt is:

-   A **full Linux system**
-   Highly **customizable**
-   Regularly **updated**
-   Designed for **advanced networking**

You can think of OpenWrt as:

>   **“Ubuntu for routers”**

------

## 2. Why Use OpenWrt?

### 2.1 Limitations of Stock Router Firmware

Most factory firmware:

-   Has limited features
-   Cannot install extra software
-   Is rarely updated
-   Locks advanced configuration

### 2.2 Advantages of OpenWrt

OpenWrt gives you:

-   ✅ Full control over routing, firewall, Wi-Fi
-   ✅ Package manager (`opkg`)
-   ✅ SSH access
-   ✅ Advanced features:
    -   VLAN
    -   VPN (WireGuard / OpenVPN)
    -   QoS / SQM
    -   Ad-blocking
    -   Mesh networking
-   ✅ Long-term community support

------

## 3. OpenWrt Architecture (Simple View)

```
+----------------------+
|  User Interface      |
|  - LuCI (Web UI)     |
|  - SSH (CLI)         |
+----------------------+
|  OpenWrt System      |
|  - BusyBox           |
|  - procd             |
|  - netifd            |
+----------------------+
|  Linux Kernel        |
+----------------------+
|  Router Hardware     |
+----------------------+
```

### Key Components

| Component   | Purpose                  |
| ----------- | ------------------------ |
| **LuCI**    | Web management interface |
| **opkg**    | Package manager          |
| **BusyBox** | Core Linux utilities     |
| **netifd**  | Network management       |
| **procd**   | Init system              |

------

## 4. Supported Devices

OpenWrt runs on:

-   Home routers
-   Travel routers
-   Mini PCs
-   Virtual machines
-   Raspberry Pi

### Check Compatibility

Always check:

```
https://openwrt.org/toh/start
```

Look for:

-   Flash size
-   RAM size
-   Supported version
-   Installation method

------

## 5. How OpenWrt Is Installed

### 5.1 Common Installation Methods

| Method         | When Used                  |
| -------------- | -------------------------- |
| Web upgrade    | Stock firmware supports it |
| TFTP           | Recovery mode              |
| Serial console | Advanced / bricked devices |
| SD card        | Raspberry Pi               |

⚠️ Installing the wrong firmware **can brick your router**.

------

## 6. First Boot Experience

After installation:

### 6.1 Default Access

-   **IP address:** `192.168.1.1`
-   **Username:** `root`
-   **Password:** *(empty)*

### 6.2 First Things to Do

1.  Set root password
2.  Configure WAN
3.  Enable Wi-Fi
4.  Update package list

------

## 7. LuCI Web Interface

LuCI is OpenWrt’s web UI.

### Key Sections

| Menu     | Description             |
| -------- | ----------------------- |
| Status   | System & network status |
| Network  | Interfaces, Wi-Fi, DHCP |
| System   | Time, users, startup    |
| Services | Installed services      |
| Firewall | Zones, rules, NAT       |

LuCI makes OpenWrt usable **without command-line knowledge**.

------

## 8. Command Line Basics (SSH)

### 8.1 Connect via SSH

```bash
ssh root@192.168.1.1
```

### 8.2 Useful Commands

| Command               | Purpose             |
| --------------------- | ------------------- |
| `opkg update`         | Update package list |
| `opkg install xxx`    | Install package     |
| `opkg list-installed` | List packages       |
| `reboot`              | Reboot system       |
| `logread`             | View system logs    |

------

## 9. Package Management with `opkg`

OpenWrt uses **opkg**, similar to `apt` or `yum`.

### Example

```bash
opkg update
opkg install htop
```

Common packages:

-   `luci-app-wireguard`
-   `luci-app-openvpn`
-   `luci-app-adblock`
-   `luci-app-sqm`

------

## 10. Network Configuration Basics

### Interfaces

OpenWrt uses logical interfaces:

-   `LAN`
-   `WAN`
-   `WAN6`

Each interface includes:

-   Protocol (DHCP, PPPoE, Static)
-   Firewall zone
-   Physical device

### Wi-Fi

Wi-Fi is **disabled by default** after installation.
You must:

1.  Set SSID
2.  Set encryption
3.  Enable radio

------

## 11. Firewall Concept (Very Important)

OpenWrt firewall is **zone-based**.

### Common Zones

| Zone | Purpose                  |
| ---- | ------------------------ |
| LAN  | Trusted internal network |
| WAN  | Untrusted internet       |

Default rule:

```
LAN → WAN : allowed
WAN → LAN : blocked
```

This provides strong security by default.

------

## 12. Common Use Cases

OpenWrt is often used for:

-   Home router replacement
-   VPN gateway
-   Ad-blocking router
-   Smart home network isolation
-   Campus / dorm networking
-   Learning networking & Linux

------

## 13. When OpenWrt Is NOT Recommended

Avoid OpenWrt if:

-   Your router has very small flash (<8MB)
-   You only want “plug and play”
-   You are afraid of troubleshooting

------

## 14. Learning Path Recommendation

For beginners:

1.  Learn LuCI basics
2.  Understand WAN / LAN
3.  Learn opkg
4.  Try SSH
5.  Configure VPN
6.  Learn firewall rules

------

## 15. Summary

OpenWrt is:

-   A powerful Linux-based router OS
-   Highly flexible and customizable
-   Ideal for learning networking
-   Best for users who want control

If you know basic Linux, OpenWrt will feel **very natural**.

