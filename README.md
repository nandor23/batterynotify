# batterynotify

A battery warning program that sends a notification when the battery percentage reaches a certain level. This is a modified bash script, written by [Eric Murphy](https://github.com/ericmurphyxyz/dotfiles/blob/master/.local/bin/batterynotify). The `batterynotify` script should be added to the `PATH` in order to enable custom battery threshold configuration from the terminal.

## Tested

It was only tested on EndeavourOS with GNOME desktop environment, but the script must function on any other distro.

## Dependencies

- [**dunst**](https://github.com/dunst-project/dunst)
- [**cronie**](https://github.com/cronie-crond/cronie)
- [**acpi**](https://sourceforge.net/projects/acpiclient)

## Features

There are 2 notifications: when the battery is low and when it is full. 

By default, it alerts the user when the battery reaches `30%` or `80%`. We can edit both thresholds by calling the script with the proper flags:

| Flag | Description |
| --- | --- |
| -l | Set the battery low warning level |
| -f | Set the battery full warning level |

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
3. Give executable permission to the script and add it to the PATH:
   ```bash
   cp batterynotify /usr/bin/
   ```
4. Set the script as a cron job, by running the `crontab -e` command. Add the line: `*/3 * * * * /usr/bin/batterynotify` - the script will be executed in every 3 minute. You can change it to another value.

   On Arch based systems the `cronie.service` needs to be enabled:
   ```bash
   systemctl enable cronie.service
   systemctl start cronie.service
   ``` 
