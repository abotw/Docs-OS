# Pi OS: Wireless Network

## 1. Prerequisites

Before starting, make sure you have:

-   A Raspberry Pi with **Raspberry Pi OS installed**
-   An **SD card** already flashed with Raspberry Pi OS
-   A **Wi-Fi network name (SSID)** and **password**
-   Another computer (Windows / macOS / Linux)
-   SSH access to the Raspberry Pi (usually via **Ethernet** for the first login)

------

## 2. Connect to Raspberry Pi via SSH

First, connect the Raspberry Pi to your router using an **Ethernet cable**.

On your computer, open a terminal and run:

```bash
ssh pi@raspberrypi.local
```

or using IP address:

```bash
ssh pi@192.168.1.100
```

Default credentials (if unchanged):

-   Username: `pi`
-   Password: `raspberry`

>   If SSH is not enabled, create an empty file named `ssh` in the SD card **boot partition** before booting.

------

## 3. Check Wi-Fi Interface

After logging in, verify that the wireless interface exists:

```bash
ip link
```

You should see something like:

```text
wlan0
```

If `wlan0` is missing, your Pi may not support Wi-Fi or drivers are not loaded.

------

## 4. Method 1 (Recommended): Use `raspi-config`

This is the **easiest and safest** way for beginners.

Run:

```bash
sudo raspi-config
```

Navigate using arrow keys:

```
System Options
  └── Wireless LAN
```

Then:

1.  Enter your **Wi-Fi country** (important for regulations)
2.  Enter **SSID (Wi-Fi name)**
3.  Enter **Wi-Fi password**

Select **Finish**, then reboot:

```bash
sudo reboot
```

------

## 5. Method 2: Configure Wi-Fi Manually (CLI)

If you prefer manual configuration or `raspi-config` is unavailable, follow this method.

### 5.1 Edit Wi-Fi Configuration File

Open the configuration file:

```bash
sudo nano /etc/wpa_supplicant/wpa_supplicant.conf
```

Add the following at the end:

```conf
country=US

network={
    ssid="Your_WiFi_Name"
    psk="Your_WiFi_Password"
}
```

>   Replace:
>
>   -   `US` with your country code (e.g. `CN`, `JP`, `GB`)
>   -   `Your_WiFi_Name` with your SSID
>   -   `Your_WiFi_Password` with your password

Save and exit:

-   `Ctrl + O` → Enter
-   `Ctrl + X`

------

### 5.2 Restart Network Services

Apply the configuration:

```bash
sudo wpa_cli -i wlan0 reconfigure
```

Or reboot:

```bash
sudo reboot
```

------

## 6. Verify Wi-Fi Connection

After reboot, reconnect via **Ethernet or Wi-Fi** and run:

```bash
ip addr show wlan0
```

If you see an IP address like:

```text
inet 192.168.1.23
```

🎉 **Wi-Fi is working!**

You can also test internet connectivity:

```bash
ping -c 3 google.com
```

------

## 7. Disable Ethernet (Optional)

Once Wi-Fi is confirmed, you can unplug the Ethernet cable.
Find the new IP address via your router or use:

```bash
hostname -I
```

------

## 8. Common Problems & Fixes

### ❌ Wi-Fi not connecting

-   Check SSID and password spelling

-   Ensure `country=` is set correctly

-   Try:

    ```bash
    sudo rfkill unblock wifi
    ```

### ❌ No `wlan0` interface

-   Your Raspberry Pi model may not support Wi-Fi
-   USB Wi-Fi adapter drivers may be missing

### ❌ Still cannot connect

Check logs:

```bash
journalctl -u wpa_supplicant
```

------

## 9. Summary

| Method         | Difficulty | Recommended |
| -------------- | ---------- | ----------- |
| `raspi-config` | ⭐ Easy     | ✅ Yes       |
| Manual config  | ⭐⭐ Medium  | Optional    |

------

## 10. Next Steps

-   Set up **static IP**
-   Enable **VNC**
-   Configure **auto-connect Wi-Fi**
-   Secure SSH with **key-based authentication**