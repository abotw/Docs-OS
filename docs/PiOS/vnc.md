# Pi OS: VNC

## 1. What Is VNC?

**VNC (Virtual Network Computing)** lets you **control your Raspberry Pi’s desktop remotely** from another computer (Windows, macOS, or Linux) over the network.

Raspberry Pi OS includes **RealVNC Server** by default, so no extra installation is usually needed.

------

## 2. Prerequisites

Before starting, make sure:

-   Raspberry Pi is running **Raspberry Pi OS (with desktop)**
-   Raspberry Pi is **connected to the network** (Wi-Fi or Ethernet)
-   You can:
    -   Access the Pi locally (monitor + keyboard), **or**
    -   Log in via SSH

------

## 3. Enable VNC on Raspberry Pi OS (GUI Method)

### Step 1: Open Raspberry Pi Configuration

1.  Click the **Raspberry Pi menu** (top-left)
2.  Select **Preferences**
3.  Click **Raspberry Pi Configuration**

### Step 2: Enable VNC

1.  Switch to the **Interfaces** tab
2.  Find **VNC**
3.  Select **Enable**
4.  Click **OK**

✅ VNC Server is now running.

------

## 4. Enable VNC via Command Line (SSH / Terminal Method)

If you don’t have a monitor attached, use this method.

### Step 1: Open Terminal or SSH into Pi

```bash
ssh pi@<raspberry-pi-ip>
```

(Default user may be `pi` or your custom username.)

### Step 2: Run Raspberry Pi Configuration Tool

```bash
sudo raspi-config
```

### Step 3: Enable VNC

1.  Select **Interface Options**
2.  Select **VNC**
3.  Choose **Yes**
4.  Select **OK**
5.  Exit

------

## 5. Verify VNC Service Status

Check whether the VNC server is running:

```bash
systemctl status vncserver-x11-serviced
```

You should see:

```text
Active: active (running)
```

If not running, start it manually:

```bash
sudo systemctl enable vncserver-x11-serviced
sudo systemctl start vncserver-x11-serviced
```

------

## 6. Find Raspberry Pi IP Address

You need the Pi’s IP address to connect.

### Method 1: From Raspberry Pi

```bash
hostname -I
```

Example output:

```text
192.168.1.120
```

### Method 2: From Router

-   Log into your router admin page
-   Find **DHCP / Connected Devices**
-   Look for `raspberrypi`

------

## 7. Connect from Another Computer

### 7.1 Install VNC Viewer

Download **RealVNC Viewer** on your client computer:

-   https://www.realvnc.com/en/connect/download/viewer/

Available for:

-   Windows
-   macOS
-   Linux

------

### 7.2 Connect to Raspberry Pi

1.  Open **VNC Viewer**

2.  Enter the Pi’s IP address:

    ```
    192.168.1.120
    ```

3.  Press **Enter**

4.  Click **Continue** (security warning is normal)

5.  Enter:

    -   **Username**: Pi username
    -   **Password**: Pi password

🎉 You should now see the Raspberry Pi desktop.

------

## 8. Common Beginner Problems & Fixes

### Problem 1: Black Screen After Connecting

**Cause**: No active desktop session.

**Fix**:

-   Ensure Raspberry Pi OS **with desktop** is installed

-   Reboot the Pi:

    ```bash
    sudo reboot
    ```

------

### Problem 2: Connection Refused

**Check**:

```bash
systemctl status vncserver-x11-serviced
```

If stopped:

```bash
sudo systemctl start vncserver-x11-serviced
```

------

### Problem 3: Slow Performance

**Suggestions**:

-   Use **Ethernet** instead of Wi-Fi
-   Lower resolution:
    -   Raspberry Pi Configuration → Display → Resolution
-   Close unnecessary programs

------

## 9. (Optional) Start VNC Automatically on Boot

Usually enabled by default, but you can confirm:

```bash
sudo systemctl enable vncserver-x11-serviced
```

------

## 10. Security Tips (Important for Beginners)

-   **Change default password**

    ```bash
    passwd
    ```

-   Do **NOT expose VNC directly to the internet**

-   Use VNC **only in local network**, or via **SSH tunnel**

------

## 11. Summary

You have learned how to:

-   Enable VNC in Raspberry Pi OS
-   Start and check VNC service
-   Find Raspberry Pi IP address
-   Connect using VNC Viewer
-   Troubleshoot common problems

VNC is one of the easiest ways to manage a Raspberry Pi without a monitor.

