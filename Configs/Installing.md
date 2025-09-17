SSH into your printer and run the installation script for the Klipper-Toolchanger plugin using the following command:
```
wget -O - https://raw.githubusercontent.com/printicus/Klipper-Toolchanger-for-Klicky-Changer/main/install.sh | bash
```
This script will download the Klipper-Toolchanger plugin to your RaspberryPi home directory, and symlink the files in the Klipper extra folder.

- Copy "Klicky-Probe", "Klipper-Toolchanger" and "Toolheads" folders from this repo to your printer config folder.
- Copy "My_MACROS.cfg" and "prime_lines.cfg" to your printer config folder.
- Ad the lines from this "printer.cfg" to your "printer.cfg". Use these macros to replace your printer.cfg macros.
- Delete, or comment out, the [probe] section from your printer.cfg file. Each toolhead config file will have its own probe section.
- Reboot your printer

Optional, ad this to your moonraker.conf to enable automatic updates:

```
[update_manager klipper-toolchanger]
type: git_repo
channel: dev
path: ~/klipper-toolchanger
origin: https://github.com/printicus/Klipper-Toolchanger-for-Klicky-Changer.git
managed_services: klipper
primary_branch: main
```
