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
