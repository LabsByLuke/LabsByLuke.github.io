# Raspberry Pi ProtonVPN Setup — Lab 2

## 📌 Overview
This lab builds on [Lab 1](raspberrypi_setup_readme.md), configuring the Raspberry Pi 5 to connect securely to ProtonVPN using **WireGuard**.  
At the end of this lab, the Pi routes all its own traffic through ProtonVPN.

---

## 📚 Table of Contents
1. [Objective](#1-objective)  
2. [Equipment](#2-equipment)  
3. [Procedure](#3-procedure)  
   - [Step 1 — Update & Secure the Pi](#step-1--update--secure-the-pi)  
   - [Step 2 — Install WireGuard](#step-2--install-wireguard)  
   - [Step 3 — Obtain ProtonVPN Config File](#step-3--obtain-protonvpn-config-file)  
   - [Step 4 — Transfer Config File to Pi](#step-4--transfer-config-file-to-pi)  
   - [Step 5 — Test VPN Connection](#step-5--test-vpn-connection)  
4. [Results](#4-results)  
5. [Key Takeaways](#5-key-takeaways)  
6. [Future Work](#6-future-work)  

---

## 1. Objective
- Configure the Raspberry Pi as a ProtonVPN client using WireGuard.  
- Verify encrypted traffic routing through ProtonVPN exit server.  
- Build foundation for turning the Pi into a VPN router (Labs 3–4).  

---

## 2. Equipment
- Raspberry Pi 5 (configured from Lab 1).  
- ProtonVPN Plus account (for WireGuard configs).  
- Laptop/desktop (Windows 11 with SSH + FileZilla).  
- ProtonVPN WireGuard configuration file.  

---

## 3. Procedure

### Step 1 — Update & Secure the Pi
Updated all packages and hardened SSH (keys already in place).  
```bash
sudo apt update && sudo apt upgrade -y
```

---

### Step 2 — Install WireGuard
Installed WireGuard VPN tools on the Pi:  
```bash
sudo apt install wireguard -y
```

![WireGuard install](images/pivpn/wireguard_install.png)

---

### Step 3 — Obtain ProtonVPN Config File
Generated a **Netherlands server WireGuard config** (`netherlands1-NL-567.conf`) via the ProtonVPN dashboard.  

![ProtonVPN config download](images/pivpn/createconfigfile.png)

---

### Step 4 — Transfer Config File to Pi
Used **FileZilla** with SSH keys to transfer the `.conf` file from Windows to the Pi’s home directory.  

![FileZilla setup](images/pivpn/filezillasetup.png)  
![File transferred](images/pivpn/filesentzilla.png)

---

### Step 5 — Test VPN Connection

1. **Move config into WireGuard directory and rename to wg0.conf**:  
```bash
sudo mv ~/netherlands1-NL-567.conf /etc/wireguard/wg0.conf
```

2. **Start VPN tunnel**:  
```bash
sudo wg-quick up wg0
```

At first, `resolvconf` was missing, causing an error:  
```bash
resolvconf: command not found
```
Fixed by installing:  
```bash
sudo apt install resolvconf -y
```

![Resolvconf install](images/pivpn/resolv.png)

3. **Retry connection** — tunnel established successfully:  
```bash
sudo wg-quick up wg0
```

![Tunnel active](images/pivpn/ranwg0.png)

4. **Check public IP** — confirmed Netherlands exit server:  
```bash
curl ifconfig.me
```
Output:  
```
103.69.224.159
```

---

## 4. Results
- ProtonVPN connection established using WireGuard.  
- Pi traffic routed through ProtonVPN Netherlands server.  
- Resolved dependency issue (`resolvconf`) during setup.  

---

## 5. Key Takeaways
- WireGuard provides a lightweight, fast VPN client ideal for the Raspberry Pi.  
- File transfer tools (FileZilla with SSH keys) simplify moving configs securely.  
- Verifying public IP ensures tunnel routing works as expected.  
- Troubleshooting missing dependencies is part of real-world sysadmin work.  

---

## 6. Future Work
- **Lab 3:** Configure Pi with static LAN IP, auto-start ProtonVPN on boot, add kill switch.  
- **Lab 4:** Convert Pi into a VPN router (subnet, DHCP, NAT).  
- Optional: add **Pi-hole** for DNS ad-blocking and monitoring dashboards.  

---

## 🔗 Next Steps
Proceed to **Lab 3 — Static IP, Auto-Connect, and Kill Switch**.
