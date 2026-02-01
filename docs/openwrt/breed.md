---
title: Breed
status: draft
---

## 1. What Is Breed?

**Breed** is a **third-party bootloader** commonly used on embedded routers (especially **MediaTek / MTK** devices).

Think of it as the **router equivalent of a PC BIOS/UEFI**, but much more powerful and user-friendly.

### What Breed can do

-   Flash **OpenWrt / LEDE / stock firmware**
-   Backup and restore router partitions
-   Recover a **bricked router**
-   Flash firmware **via a web browser**
-   Manage kernel, rootfs, and full firmware images

### Why people like Breed

-   Web-based (no serial cable required)
-   Much safer than vendor bootloaders
-   Ideal for firmware developers and beginners

------

## 2. When Do You Need Breed?

You typically use Breed when you want to:

-   Install **OpenWrt / LEDE**
-   Recover from a **failed firmware flash**
-   Switch between **official firmware and OpenWrt**
-   Experiment with custom builds

If you already use OpenWrt daily, **Breed is your safety net**.

------

## 3. What Is “Breed (Web)”?

Breed supports **multiple access methods**, but the most common is:

>   **Breed Web UI** – a small web page hosted by the bootloader itself

This allows you to:

-   Open a browser
-   Upload firmware
-   Flash safely
-   No command line needed

------

## 4. Supported Devices (Important!)

Breed is **device-specific**.

Before using Breed, you must confirm:

-   Your **router model**
-   Your **SoC (CPU)**

### Common supported platforms

-   MediaTek MT7620 / MT7621 / MT7628
-   MT7981 / MT7986 (some newer devices)
-   Many Xiaomi, GL.iNet, Newifi routers

⚠️ **Never flash a Breed image for another model.**

------

## 5. How Breed Works (Simple Explanation)

Boot sequence:

```
Power on
 ↓
Breed bootloader
 ↓
Firmware (OpenWrt / Stock)
```

Breed runs **before** the firmware, so even if the firmware is broken, Breed still works.

------

## 6. How to Enter Breed Web Mode

### Method 1: Hardware Reset Button (Most Common)

1.  Power off the router
2.  **Press and hold the RESET button**
3.  Power on the router
4.  Keep holding RESET for **5–10 seconds**
5.  Release the button

If successful:

-   Router does **not boot normally**
-   Breed Web UI becomes active

------

### Method 2: From OpenWrt (If Installed)

Some routers allow entering Breed via command:

```bash
reboot
```

Then hold RESET immediately during reboot.

(Exact behavior depends on device.)

------

## 7. Connecting to Breed Web Interface

### Step 1: Set Your Computer IP

Breed usually uses a **static IP**, commonly:

```
Router (Breed): 192.168.1.1
```

Set your PC manually:

| Setting | Value         |
| ------- | ------------- |
| IP      | 192.168.1.2   |
| Netmask | 255.255.255.0 |
| Gateway | (leave empty) |

------

### Step 2: Connect via Ethernet

-   Use a **LAN cable**
-   Connect PC → router LAN port
-   Wi-Fi usually does NOT work in Breed mode

------

### Step 3: Open the Web Page

Open browser and visit:

```
http://192.168.1.1
```

If successful, you will see:

>   **Breed Web Recovery Console**

------

## 8. Breed Web Interface Overview

Typical sections include:

### 1. Firmware Update

-   Flash full firmware
-   Flash kernel or rootfs separately

### 2. Partition Management

-   View flash layout
-   Backup partitions
-   Restore partitions

### 3. System Info

-   Flash size
-   RAM
-   CPU info

### 4. Environment Variables

-   Boot arguments
-   Advanced users only

------

## 9. Flashing Firmware Using Breed (Beginner Safe Way)

### Step 1: Prepare Firmware

-   Download **correct firmware** for your router
-   Usually a `.bin` file
-   Prefer **sysupgrade** or **factory** image as recommended

------

### Step 2: Upload Firmware

In Breed Web UI:

1.  Go to **Firmware Update**
2.  Choose firmware file
3.  Select **Full Flash** (recommended for beginners)
4.  Click **Upload**

------

### Step 3: Flash and Reboot

-   Wait patiently (1–3 minutes)
-   **Do NOT power off**
-   Router reboots automatically

------

## 10. Backup Before Flashing (Highly Recommended)

Before flashing anything:

1.  Open **Partition Backup**
2.  Backup:
    -   Bootloader
    -   Factory
    -   EEPROM / ART
3.  Save files to your PC

These backups can **save your router forever**.

------

## 11. Common IP Addresses Used by Breed

| IP           | Usage        |
| ------------ | ------------ |
| 192.168.1.1  | Most common  |
| 192.168.0.1  | Some devices |
| 192.168.99.1 | Rare         |

Check your router documentation if unsure.

------

## 12. Common Problems and Fixes

### Cannot open 192.168.1.1

-   Check PC IP configuration
-   Disable Wi-Fi
-   Try another LAN port
-   Try another browser

------

### Flash fails

-   Wrong firmware image
-   Mismatched flash layout
-   Try **full flash** instead of partial

------

### Router boot loops

-   Enter Breed again
-   Restore backup
-   Flash known-good firmware

------

## 13. Safety Rules (Very Important)

✅ Always use firmware for **your exact model**
✅ Always backup partitions first
❌ Never flash bootloader unless required
❌ Never interrupt power during flashing

------

## 14. Breed vs U-Boot (Simple Comparison)

| Feature           | Breed | Stock U-Boot |
| ----------------- | ----- | ------------ |
| Web UI            | ✅     | ❌            |
| Easy recovery     | ✅     | ❌            |
| Beginner friendly | ✅     | ❌            |
| Brick risk        | Low   | High         |

------

## 15. Summary

-   **Breed** is a powerful router bootloader
-   **Breed Web UI** makes flashing firmware easy
-   It is the **best recovery tool** for OpenWrt users
-   Learn it once, save your router many times

