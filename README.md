# 🌐 Edu-WiFi Omarchy Setup

This guide shows you how to configure **eduroam** Wi-Fi on Omarchy/Linux using the **iwd (iNet wireless daemon)**.

---

## ⚡ Requirements

* Linux with `iwd` installed
* Sudo/root privileges
* Your university **eduroam email** and **password**

---

## 🔧 Setup Steps

### 1️⃣ Enable & start iwd

```bash
sudo systemctl enable iwd.service
sudo systemctl start iwd.service
```

### 2️⃣ Scan and check available networks

```bash
iwctl
[iwd]# device list
[iwd]# station wlan0 scan
[iwd]# station wlan0 get-networks
```

You should see `eduroam` in the list.

### 3️⃣ Create 802.1X config file

Create the file:

```bash
sudo nano /var/lib/iwd/eduroam.8021x
```

Paste the following template (replace with your **student email** and **password**):

```
[Security]
EAP-Method=PEAP
EAP-Identity=yourstudentemail@youruniversity.edu
EAP-PEAP-Phase2-Method=MSCHAPV2
EAP-Password=yourpassword
```

---

### 4️⃣ Fix permissions (important!)

```bash
sudo chmod 600 /var/lib/iwd/eduroam.8021x
sudo chown root:root /var/lib/iwd/eduroam.8021x
```

---

### 5️⃣ Connect to eduroam

Restart `iwd` and connect:

```bash
sudo systemctl restart iwd
iwctl
[iwd]# station wlan0 connect eduroam
```

---

## ✅ Verify connection

```bash
ping -c 3 8.8.8.8
```

If replies come back, you’re online 🎉

---

## 📌 Notes

* `iwd` will remember the configuration for future reboots.
* If connection fails, check file permissions again.
* Make sure your university credentials are correct.

---

👨‍💻 Author: [Muhammad-Taaha](https://github.com/Muhammad-Taaha)
📡 Project: **edu-wifi-omarchy**
