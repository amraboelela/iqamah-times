# Iqamah Times

General instructions: https://albara.ramli.net/iqamah/

## Install
To install on Raspberry Pi 4 (or 5):

- Test this link: https://albara.ramli.net/iqamah/screen.php?city=merced&size=2

**Note:** You will need to replace `merced` with your own city, if your city doesn't exist, please contact albara@ramli.net to add your city. This is the link we will use in the below instructions, so make sure you replace `merced` with your own city in the below instructions as well.

### Check if using LXDE or Wayland
Using the terminal app, run:
```bash
echo $XDG_CURRENT_DESKTOP
```
If LXDE is running, it should output:
```
LXDE
```

If Wayland is running, it should output:
```
labwc:wlroots
```

### If using LXDE
Then run:
```
sudo nano /etc/rc.local
```

Then add this line after replacing `merced` with your own city, before `exit 0` line:
```
chromium-browser --start-fullscreen https://albara.ramli.net/iqamah/screen.php?city=merced&size=2
```

#### Another method

```
sudo mousepad /etc/xdg/lxsession/LXDE-pi/autostart
```

Then add this line after replacing `merced` with your own city.
```
chromium-browser --start-fullscreen https://albara.ramli.net/iqamah/screen.php?city=merced&size=2
```

### If using Wayland

1. Open or create the **Labwc startup file**:
   ```bash
   nano ~/.config/labwc/autostart
   ```
2. Add this line after replacing `merced` with your own city.
   ```
   chromium-browser --enable-features=UseOzonePlatform --ozone-platform=wayland --start-fullscreen --noerrdialogs --disable-infobars --incognito https://albara.ramli.net/iqamah/screen.php?city=merced&size=2 &
   ```
3. Save and exit (`CTRL + X`, then `Y`, then `Enter`).

### Change display to portrait

To rotate the display to **portrait mode** on your Raspberry Pi using the **GUI (Raspberry Pi OS / Roseberry)**, follow these steps:

1. **Open the "Screen Configuration" Tool**  
   - Click on the **Raspberry Pi menu** (top-left corner).  
   - Go to **Preferences** → **Screen Configuration**.

2. **Select the Display**  
   - Click on the **display** you want to rotate.

3. **Change the Orientation**  
   - In the menu bar, go to **"Orientation"**.
   - Choose **"Right"** (90°) or **"Left"** (270°) for portrait mode.
   - Click **"Apply"**.

4. **Confirm the Rotation**  
   - A prompt will appear asking if you want to keep the changes. Click **"OK"**.

### Mute the machine
To prevent any atahn or sound to come out of the Rasberry machine:

**Method 1: Mute from the Taskbar**
1. Look for the **speaker icon** in the **top-right corner** of the screen.  
2. **Right-click** the speaker icon and select **Mute Audio**.  
3. This setting should persist after rebooting (but may not always).  

**Method 2: Disable Audio in Raspberry Pi Settings**
1. Open the **Raspberry Pi menu** (top-left).  
2. Go to **Preferences** → **Audio Device Settings**.  
3. Set the **output device** to "Off" or mute all volume sliders.  
4. Click **Apply**, then **OK**.  

### Restart the machine
At the end you need restart the machine:
```
$ sudo reboot
```

To **reboot** your Raspberry Pi from the **GUI menu**, follow these steps:  

1. Click on the **Raspberry Pi menu** (top-left corner of the screen).  
2. Select **Logout**.  
3. In the popup window, click **Restart**.  




