# iqamah-times

General instructions: https://albara.ramli.net/iqamah/

## Install
To install on Raspberry Pi 4 (or 5):

```
sudo nano /etc/rc.local
```

Then add, this line before `exit 0`:
```
chromium-browser --start-fullscreen https://albara.ramli.net/iqamah/screen.php?city=merced&size=7
```

### Another method
This didn't work with me though!

```
sudo mousepad /etc/xdg/lxsession/LXDE-pi/autostart
```

Add:
```
chromium-browser --start-fullscreen https://albara.ramli.net/iqamah/screen.php?city=merced&size=7
```

Restart the machine:
```
$ sudo reboot
```

If you're trying to **automatically start Chromium on boot** on your Raspberry Pi 5 and it’s not working, try these steps:

---

### **1. Use Autostart Method (Recommended)**
1. Open a terminal and edit the autostart file:
   ```bash
   mkdir -p ~/.config/lxsession/LXDE-pi
   nano ~/.config/lxsession/LXDE-pi/autostart
   ```
2. Add the following line at the end to start Chromium in kiosk mode (or normal mode):
   ```
   @chromium-browser --start-fullscreen --noerrdialogs --disable-infobars --incognito https://www.google.com
   ```
   *(Change the URL as needed.)*
3. Save and exit (`CTRL + X`, then `Y`, then `Enter`).

4. Restart your Pi:
   ```bash
   sudo reboot
   ```

---

### **2. Use Systemd Service (Alternative)**
If the autostart method doesn’t work, try a **systemd service**:

1. Create a new service file:
   ```bash
   sudo nano /etc/systemd/system/chromium-autostart.service
   ```
2. Add the following:
   ```ini
   [Unit]
   Description=Start Chromium on boot
   After=graphical.target

   [Service]
   Environment=DISPLAY=:0
   ExecStart=/usr/bin/chromium-browser --start-fullscreen --noerrdialogs --disable-infobars --incognito https://www.google.com
   Restart=always
   User=pi

   [Install]
   WantedBy=graphical.target
   ```
3. Save and exit (`CTRL + X`, then `Y`, then `Enter`).

4. Enable and start the service:
   ```bash
   sudo systemctl enable chromium-autostart
   sudo systemctl start chromium-autostart
   ```

5. Reboot:
   ```bash
   sudo reboot
   ```

---


To check if **LXDE (Lightweight X11 Desktop Environment)** is installed on your Raspberry Pi, try the following methods:

---

### **1. Check Installed Packages**
Run this command in the terminal:
```bash
dpkg -l | grep lxde
```
If LXDE is installed, you should see package names like:
```
ii  lxde ...
ii  lxde-common ...
ii  lxde-core ...
```
If nothing appears, LXDE is **not installed**.

---

### **2. Check if LXDE is Running**
If you are in the GUI, run:
```bash
echo $XDG_CURRENT_DESKTOP
```
If LXDE is running, it should output:
```
LXDE
```
If it’s empty or shows something else, then LXDE may not be running.

---

### **3. Try Manually Starting LXDE**
Run:
```bash
startx
```
If LXDE is installed but not set to start automatically, this command should launch it.

---

### **4. Install LXDE (If Missing)**
If you don’t have LXDE, install it with:
```bash
sudo apt update
sudo apt install -y lxde lxde-common lxde-core
```
Then reboot:
```bash
sudo reboot
```

Let me know if you need more help! 🚀
