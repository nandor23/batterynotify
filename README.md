# batterynotify

A battery warning program that sends a notification when the battery percentage reaches a certain level. This is a modified bash script, written by [Eric Murphy](https://github.com/ericmurphyxyz/dotfiles/blob/master/.local/bin/batterynotify). The `batterynotify` script should be added to the `PATH` in order to enable custom battery threshold configuration from the terminal.

## Tested

It was only tested on EndeavourOS with GNOME desktop environment, but the script must function on any other distro.

## Dependencies

It was only tested on EndeavourOS with GNOME desktop environment, but the script

## Features

There are 2 notifications: when the battery is low and when it is full. 

By default, it alerts the user when the battery reaches `30%` or `80%`. We can edit both thresholds by calling the script with the proper flags:

Expand All
	@@ -33,22 +33,22 @@ batterynotify -l 25 -f 70

1. Install the dependencies
2. Change the value of `DBUS_SESSION_BUS_ADDRESS` in the script to the output of the following command (without the guid):
   
   ```bash
   echo $DBUS_SESSION_BUS_ADDRESS
   ```
3. Give executable permission to the script and add it to the PATH:
   ```bash
   cp batterynotify /usr/bin/
   ```
4. Set the script as a cron job, by running the `crontab -e` command. Paste the following line to the file: `*/3 * * * * /usr/bin/batterynotify` and save it. The **3** means that the script will be executed in every 3 minute. Adjust it to your needs if it is too frequent.

   On Arch based systems the `cronie.service` needs to be enabled:
   ```bash
   systemctl enable cronie.service
   systemctl start cronie.service
   ```
5. On GNOME to run the script on startup too, the `batterynotify.desktop` file must be copied to `~/.config/autostart`:
   ```bash
   cp batterynotify.desktop ~/.config/autostart
   ```
