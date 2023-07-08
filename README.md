# batterynotify

A battery warning program that sends a notification when the battery percentage reaches a certain level. This is a modified bash script, written by [Eric Murphy](https://github.com/ericmurphyxyz/dotfiles/blob/master/.local/bin/batterynotify). The `batterynotify` script should be added to the `PATH` in order to enable custom battery threshold configuration from the terminal.

## Tested

It was only tested on EndeavourOS with GNOME desktop environment, but the script must function on any other distro.

## Dependencies

- [**dunst**](https://github.com/dunst-project/dunst)
- [**cronie**:](https://github.com/cronie-crond/cronie)
- [**acpi**:](https://sourceforge.net/projects/acpiclient)

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
