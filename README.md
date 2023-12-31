# Battery notifier for Linux

A battery alert program that sends a notification when the battery percentage reaches a certain level. This is a modified bash script, originally written by [Eric Murphy](https://github.com/ericmurphyxyz/dotfiles/blob/master/.local/bin/batterynotify). The `batterynotify` script should be added to the `PATH` in order to enable custom battery threshold configuration from the terminal.

<img src="images/battery_low.png" alt="Alt Text" width="550">
<img src="images/battery_full.png" alt="Alt Text" width="550">



## Tested

It was only tested on EndeavourOS with GNOME desktop environment, but the script should function on any other distro.

## Dependencies

- [**dunst**](https://github.com/dunst-project/dunst)
- [**cronie**](https://github.com/cronie-crond/cronie)
- [**acpi**](https://sourceforge.net/projects/acpiclient)

## Features

There are 2 notifications: when the battery is low and when it is full. 

By default, it alerts the user when the battery reaches `30%` or `80%`. We can edit both thresholds by calling the script with the proper flags:

| Flag | Description |
| --- | --- |
| **-l** | Adjust the low battery warning threshold |
| **-f** | Adjust the full battery warning threshold |

For example, to get notifications when the battery reaches `25%` and `70%`:
```bash
batterynotify -l 25 -f 70
```

## Installation

1. Install the dependencies
2. Change the value of `DBUS_SESSION_BUS_ADDRESS` in the script to the output of the following command (without the guid):
   
   ```bash
   echo $DBUS_SESSION_BUS_ADDRESS
   ```
3. **Optional!** The file where the threshold values are saved can be changed, by editing the value of `VALUES_FILE` in the script. 
4. Give executable permission to the script and add it to the PATH:
   ```bash
   cp batterynotify /usr/bin/
   ```
5. Set the script as a cron job, by running the `crontab -e` command. Paste the following line to the file: `*/3 * * * * /usr/bin/batterynotify` and save it. The **3** means that the script will be executed in every 3 minute. Adjust it to your needs if it is too frequent.

   On Arch based systems the `cronie.service` needs to be enabled:
   ```bash
   systemctl enable cronie.service
   systemctl start cronie.service
   ```
6. On GNOME, to run the script on startup too, the `batterynotify.desktop` file must be copied to `~/.config/autostart`:
   ```bash
   cp batterynotify.desktop ~/.config/autostart
   ```
