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

If `echo $XDG_CURRENT_DESKTOP` returns **`labwc:wlroots`**, that means your Raspberry Pi 5 is running **Labwc**, a Wayland-based lightweight window manager, instead of LXDE.  

Since **Labwc is Wayland-based**, Chromium might not launch automatically in the same way as it does in an **X11-based** environment like LXDE.

---

### **How to Start Chromium on Wayland (Labwc)**
Try launching Chromium with Wayland support:
```bash
chromium-browser --enable-features=UseOzonePlatform --ozone-platform=wayland
```
If Chromium works this way, you can add it to autostart.

---

### **How to Autostart Chromium on Labwc**
1. Open or create the **Labwc startup file**:
   ```bash
   nano ~/.config/labwc/autostart
   ```
2. Add the following line:
   ```
   chromium-browser --enable-features=UseOzonePlatform --ozone-platform=wayland --start-fullscreen --noerrdialogs --disable-infobars --incognito https://www.google.com &
   ```
3. Save and exit (`CTRL + X`, then `Y`, then `Enter`).

4. Restart Labwc or reboot:
   ```bash
   sudo reboot
   ```

---

### **Do You Want to Use LXDE Instead?**
If you prefer the traditional **LXDE desktop**, you can install it with:
```bash
sudo apt update
sudo apt install -y lxde lxde-common lxde-core
```
Then set it as the default session:
```bash
sudo raspi-config
```
- Go to **System Options** → **Boot/Auto Login** → **Desktop GUI**.
- Select **LXDE**.
- Reboot.

Let me know which approach you prefer! 🚀

