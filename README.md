# iqamah-times

General instructions: https://albara.ramli.net/iqamah/

## Install
To install on Raspberry Pi 4 (or 5):

### Check if using LXDE or Wayland
If you are in the GUI, run:
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

#### If using LXDE
Then run:
```
sudo nano /etc/rc.local
```

Then add, this line before `exit 0`:
```
chromium-browser --start-fullscreen https://albara.ramli.net/iqamah/screen.php?city=merced&size=7
```

#### Another method
This didn't work with me though!

```
sudo mousepad /etc/xdg/lxsession/LXDE-pi/autostart
```

Add:
```
chromium-browser --start-fullscreen https://albara.ramli.net/iqamah/screen.php?city=merced&size=7
```

***Note:*** need to replace `merced` with your own city, if your city doesn't exist, please contact albara@ramli.net to add your city.

Restart the machine:
```
$ sudo reboot
```

### If using Wayland

1. Open or create the **Labwc startup file**:
   ```bash
   nano ~/.config/labwc/autostart
   ```
2. Add the following line:
   ```
   chromium-browser --enable-features=UseOzonePlatform --ozone-platform=wayland --start-fullscreen --noerrdialogs --disable-infobars --incognito https://albara.ramli.net/iqamah/screen.php?city=merced&size=7 &
   ```
3. Save and exit (`CTRL + X`, then `Y`, then `Enter`).

4. Restart Labwc or reboot:
   ```bash
   sudo reboot
   ```

