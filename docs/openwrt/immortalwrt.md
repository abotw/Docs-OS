---
title: ImmortalWrt
status: done
---

-   <https://github.com/immortalwrt>
-   <https://firmware-selector.immortalwrt.org/>

## 1. What Is ImmortalWrt?

**ImmortalWrt** is a **community-driven fork of OpenWrt**.

In simple terms:

>   **ImmortalWrt = OpenWrt + more features + faster updates + router-user focus**

### Key characteristics

-   Based on **OpenWrt source code**
-   Maintains **additional patches and features**
-   Often includes **more LuCI apps and kernel modules**
-   Popular among users in **China / Asia**
-   Actively maintained

If OpenWrt is the *official upstream*, ImmortalWrt is a **feature-rich downstream distribution**.

## 2. ImmortalWrt vs OpenWrt (Beginner View)

| Feature           | OpenWrt   | ImmortalWrt  |
| ----------------- | --------- | ------------ |
| Official project  | ✅         | ❌ (fork)     |
| Stability         | Very high | High         |
| Release speed     | Slower    | Faster       |
| Built-in packages | Minimal   | More         |
| LuCI apps         | Basic     | Rich         |
| Beginner friendly | Medium    | **High**     |
| Community support | Global    | Asia-focused |

**For beginners**, ImmortalWrt often feels:

-   Easier to use
-   Less manual package installation
-   Better “out of the box”

## 3. When Should You Choose ImmortalWrt?

### Recommended if:

-   You want **easy setup**
-   You plan to use:
    -   **Proxy tools** (**PassWall** / SSR Plus / OpenClash)
    -   USB storage
    -   NAS / file sharing
-   Your router is **low-end or mid-range**
-   You don’t want to compile everything yourself

### Not recommended if:

-   You need **official OpenWrt certification**
-   You develop upstream OpenWrt code
-   You want the **purest minimal system**

## 4. Supported Devices

ImmortalWrt supports **most OpenWrt-supported devices**, plus some extras.

### Common platforms

-   MediaTek (MT7621 / MT7981 / MT7986)
-   Qualcomm IPQ
-   x86_64
-   Some older MIPS devices

⚠️ **Always check device model carefully**
Different hardware revisions = different firmware

## 5. Firmware Types Explained (Very Important)

When downloading ImmortalWrt firmware, you will see several files.

### Common filenames

```
immortalwrt-23.05.1-xxx-sysupgrade.bin
immortalwrt-23.05.1-xxx-factory.bin
```

### What do they mean?

| File             | Purpose                                |
| ---------------- | -------------------------------------- |
| `factory.bin`    | Flash from **stock firmware**          |
| `sysupgrade.bin` | Upgrade from **OpenWrt / ImmortalWrt** |

❗ Flashing the wrong one may **brick your router**.

## 6. Flashing ImmortalWrt (General Process)

>   The exact steps vary by router, but the **logic is always the same**.

### Method 1: From stock firmware (Web UI)

1.  Login to stock router page
2.  Firmware upgrade
3.  Upload `factory.bin`
4.  Wait patiently (do NOT power off)

### Method 2: From OpenWrt / ImmortalWrt

1.  Login to LuCI
2.  **System → Backup / Flash Firmware**
3.  Upload `sysupgrade.bin`
4.  Choose:
    -   Keep settings ❌ (recommended OFF for beginners)
5.  Flash and reboot

## 7. First Boot: What You Should Do

After flashing, ImmortalWrt will usually use:

-   IP: `192.168.1.1`
-   No password

### Step 1: Set root password

```
System → Administration
```

### Step 2: Configure WAN

```
Network → Interfaces → WAN
```

Common types:

-   DHCP (most home networks)
-   PPPoE (ISP username/password)

## 8. LuCI Interface Overview

ImmortalWrt uses **LuCI**, the web UI.

### Main menus beginners care about

-   **Status** – system info
-   **Network** – LAN / WAN / Wi-Fi
-   **System** – password, timezone, upgrade
-   **Services** – proxy, VPN, NAS, etc.

ImmortalWrt usually includes **more items under “Services”** than OpenWrt.

## 9. Package Management (opkg)

ImmortalWrt uses the same package system as OpenWrt.

### Update package list

```sh
opkg update
```

### Install a package

```sh
opkg install htop
```

### Remove a package

```sh
opkg remove htop
```

💡 ImmortalWrt often ships with:

-   More kernel modules
-   Common LuCI apps pre-enabled

## 10. ImmortalWrt Software Ecosystem

Popular built-in or available features:

-   PassWall / SSR Plus
-   OpenClash
-   USB storage & automount
-   Samba / FTP
-   WireGuard / OpenVPN
-   Ad blocking
-   QoS / SQM

This is one reason **beginners prefer ImmortalWrt**.

## 11. Upgrade Strategy (Important for Beginners)

### Safe upgrade rules

-   Always use **sysupgrade.bin**
-   Backup configs first
-   Major version upgrade → **do NOT keep settings**
-   Read changelog before upgrading

### Recommended

-   Stay on **stable releases**
-   Avoid daily snapshots unless you know what you’re doing

## 12. Common Beginner Mistakes

❌ Flashing wrong firmware file

❌ Mixing OpenWrt and ImmortalWrt feeds

❌ Forcing opkg installs (`-f`)

❌ Ignoring storage size limits

❌ Power-off during flashing

## 13. ImmortalWrt vs LEDE vs OpenWrt (Quick Summary)

-   **OpenWrt** → official, clean, minimal
-   **ImmortalWrt** → feature-rich, beginner-friendly
-   **LEDE** → legacy (now merged into OpenWrt)

👉 For **learning and daily home use**:
**ImmortalWrt is an excellent starting point**

## 14. Learning Path Recommendation

For beginners:

1.  Learn **LuCI basics**
2.  Understand **interfaces & firewall**
3.  Practice **opkg**
4.  Add one service at a time
5.  Learn sysupgrade & recovery

