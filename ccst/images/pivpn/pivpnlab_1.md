# Pi VPN Lab 1 — Raspberry Pi Setup & SSH Access

## 🎯 Objective
Documenting the successful setup of the Raspberry Pi 5 for headless operation using Raspberry Pi OS Lite, configured for secure SSH access and verified network connectivity.  
This lab forms the foundation for the future VPN and Wi-Fi configuration.

---

## 🧱 Hardware Used
- Raspberry Pi 5 (8 GB)
- Crucial C8 2 TB SSD (always attached)
- Official 27W USB-C Power Supply
- Cat 5e Ethernet cable
- PC running Windows (used for setup)

---

## 💽 Raspberry Pi Imager
- Downloaded from [raspberrypi.com/software](https://www.raspberrypi.com/software/)
- Installed on Windows
- Selected **Raspberry Pi OS Lite (64-bit)**
- Chose SSD as the install target

### Advanced Settings Configured
- Hostname set to `luza`
- SSH enabled → **Public-key authentication only**
- Username set to `luke`
- Pasted public SSH key from:
  ```
  C:\Users\luked\.ssh\id_ed25519.pub
  ```
- Locale, timezone, and keyboard set
- Options chosen:
  - ✅ Eject media when finished
  - ❌ Telemetry (off)
  - 🔇 No sound alert

The SSD was successfully flashed and safely ejected.

---

## 🔐 SSH Key Generation
- Generated SSH key pair in Windows PowerShell using:
  ```bash
  ssh-keygen -t ed25519 -C "luke@luza"
  ```
- Accepted default save location:
  ```
  C:\Users\luked\.ssh\id_ed25519
  C:\Users\luked\.ssh\id_ed25519.pub
  ```
- Left passphrase empty for convenience in lab environment.

---

## 🔌 First Boot and SSH Connection
- Inserted SSD into Pi and connected power + Ethernet.
- Located Pi IP via router’s device list.
- Connected from Windows using:
  ```bash
  ssh luke@luza.local
  ```
  or with IP:
  ```bash
  ssh luke@192.168.50.x
  ```
- Successfully authenticated using SSH key — no password prompt.

---

## 🧪 Verification and Updates
Once connected, verified Pi identity and network configuration:
```bash
hostname
ip a
```
Confirmed hostname as `luza` and valid IP on home network.

Updated system:
```bash
sudo apt update && sudo apt full-upgrade -y
```
System upgraded successfully with no errors.

---

## ✅ Lab 1 Outcome
- Raspberry Pi OS Lite installed and running from SSD
- SSH access via key confirmed working
- Network connectivity verified
- System fully updated and ready for next stage

---

The Pi is now ready for **Lab 2: Network Configuration**, where static IPs will be configured, and groundwork for the VPN Wi-Fi router setup will begin.

