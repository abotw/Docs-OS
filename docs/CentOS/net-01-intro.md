# CentOS: Net

Understanding Network Services in CentOS

## 1. What Are “Network Services”?

In CentOS, a **network service** is a **background program (daemon)** that:

-   Manages network connections
-   Provides network functionality
-   Starts automatically in the background

Examples:

-   `network` → basic network interface management
-   `NetworkManager` → **dynamic** network management
-   `sshd` → SSH remote login
-   `firewalld` → firewall service

------

## 2. Service Management Basics (systemd)

CentOS 7 uses **systemd** to manage services.

### 2.1 Common systemctl Commands

```bash
systemctl status service_name
systemctl start service_name
systemctl stop service_name
systemctl restart service_name
systemctl enable service_name
systemctl disable service_name
```

Example:

```bash
sudo systemctl status network
```

------

## 3. The `network` Service (Traditional)

### 3.1 What Is the `network` Service?

The **`network` service**:

-   Reads configuration files from
    `/etc/sysconfig/network-scripts/`
-   Brings interfaces up or down
-   Uses files like `ifcfg-ens33`

Service name:

```bash
network
```

### 3.2 Check Network Service Status

```bash
systemctl status network
```

### 3.3 Restart Network Service

```bash
sudo systemctl restart network
```

⚠️ Restarting the network service may **disconnect SSH**.

## 4. NetworkManager (Modern Network Service)

### 4.1 What Is NetworkManager?

**NetworkManager** is a more advanced network service that:

-   Supports Wi-Fi, VPN, mobile networks
-   Handles **dynamic** network changes
-   Is enabled by default in many systems

Service name:

```bash
NetworkManager
```

### 4.2 Check NetworkManager Status

```bash
systemctl status NetworkManager
```

### 4.3 NetworkManager Tools

| Tool    | Purpose                 |
| ------- | ----------------------- |
| `nmcli` | Command-line management |
| `nmtui` | Text-based UI           |

Example:

```bash
nmtui
```

## 5. `network` vs `NetworkManager`

| Item                      | network     | NetworkManager |
| ------------------------- | ----------- | -------------- |
| Config style              | ifcfg files | dynamic        |
| Server usage              | Common      | Common         |
| Desktop usage             | Rare        | Common         |
| DHCP support              | Yes         | Yes            |
| Recommended for beginners | Yes         | Yes            |

⚠️ **Do not manage the same interface with both at the same time.**

## 6. SSH Service (`sshd`)

### 6.1 What Is SSH?

**SSH** allows you to:

-   Log in remotely
-   Execute commands securely

Service name:

```bash
sshd
```

------

### 6.2 Check SSH Service

```bash
systemctl status sshd
```

Start SSH:

```bash
sudo systemctl start sshd
sudo systemctl enable sshd
```

------

## 7. Firewall Service (`firewalld`)

### 7.1 What Is firewalld?

`firewalld` controls:

-   Which ports are open
-   Which services are allowed

Service name:

```bash
firewalld
```

### 7.2 Check Firewall Status

```bash
systemctl status firewalld
```

### 7.3 Allow SSH Traffic

```bash
sudo firewall-cmd --add-service=ssh --permanent
sudo firewall-cmd --reload
```

## 8. DNS and Name Resolution Services

### 8.1 `/etc/resolv.conf`

Used for DNS:

```bash
cat /etc/resolv.conf
```

Example:

```text
nameserver 8.8.8.8
```

This file is often **managed automatically**.

------

### 8.2 Name Service Switch (`nsswitch.conf`)

```bash
/etc/nsswitch.conf
```

Controls how the system resolves:

-   hostnames
-   users
-   groups

------

## 9. Common Network-Related Services Summary

| Service          | Purpose                    |
| ---------------- | -------------------------- |
| `network`        | Traditional network setup  |
| `NetworkManager` | Dynamic network management |
| `sshd`           | Remote login               |
| `firewalld`      | Firewall                   |
| `chronyd`        | Time synchronization       |
| `rsyslog`        | Network logging            |

------

## 10. Checking Open Ports

```bash
ss -tuln
```

Or:

```bash
netstat -tuln
```

------

## 11. Typical Beginner Workflow

1.  Configure `ifcfg-ens33`
2.  Restart `network`
3.  Verify IP and route
4.  Ensure `sshd` is running
5.  Open firewall ports if needed

------

## 12. Common Beginner Mistakes

❌ Restarting network over SSH without caution
❌ Disabling NetworkManager incorrectly
❌ Forgetting firewall rules
❌ Mixing `network` and `NetworkManager`

------

## 13. Troubleshooting Checklist

-   `systemctl status network`
-   `ip addr`
-   `ip route`
-   `ping gateway`
-   `ping 8.8.8.8`
-   `journalctl -u network`

------

## 14. Summary

-   Network services run in the background
-   Managed by `systemctl`
-   `network` and `NetworkManager` manage interfaces
-   `sshd` enables remote access
-   `firewalld` controls traffic

Understanding network services is **essential for server administration** 👍