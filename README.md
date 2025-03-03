# Iqamah Times

General instructions: https://albara.ramli.net/iqamah/

## Install
To install on Raspberry Pi 4 (or 5):

- Test this link: https://albara.ramli.net/iqamah/screen.php?city=merced&size=7

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

- **If using LXDE**
Then run:
```
sudo nano /etc/rc.local
```

Then add this line after replacing `merced` with your own city, before `exit 0` line:
```
chromium-browser --start-fullscreen https://albara.ramli.net/iqamah/screen.php?city=merced&size=7
```

#### Another method

```
sudo mousepad /etc/xdg/lxsession/LXDE-pi/autostart
```

Then add this line after replacing `merced` with your own city.
```
chromium-browser --start-fullscreen https://albara.ramli.net/iqamah/screen.php?city=merced&size=7
```

- **If using Wayland**

1. Open or create the **Labwc startup file**:
   ```bash
   nano ~/.config/labwc/autostart
   ```
2. Add this line after replacing `merced` with your own city.
   ```
   chromium-browser --enable-features=UseOzonePlatform --ozone-platform=wayland --start-fullscreen --noerrdialogs --disable-infobars --incognito https://albara.ramli.net/iqamah/screen.php?city=merced&size=7 &
   ```
3. Save and exit (`CTRL + X`, then `Y`, then `Enter`).

### Restart the machine
At the end you need restart the machine:
```
$ sudo reboot
```


