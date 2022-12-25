# PiEmuCD

### Turn your Pi Zero into one or more virtual USB CD-ROM drives!

PiEmuCD is a Python script that uses the Linux USB Gadget kernel modules to turn your Raspberry Pi Zero (W) into one or more emulated USB CD-ROM drives.

**Documentation is a work in progress.**

## Installation

1. **Prepare the SD Card**

-   Flash Raspberry Pi OS Lite (Bullseye) to an SD Card (16 GB minimum recommended size)
    -   Use the Pi Imager tool to preconfigure hostname, login and locale
-   Use a partitioning tool to:
    -   Extend system partition to 4 GiB
    -   Create new partition, exFAT for the rest of the SD card -> this partition is called the **image store**.
-   Edit files from boot partition
    -   Add `dtoverlay=dwc2` to `config.txt`
    -   From `cmdline.txt` emove `quiet` and `init=/usr/lib/raspberrypi-sys-mods/firstboot` to prevent the OS from resizing the root partition on first boot

2. **Configure the Raspberry Pi**

-   Connect to the Pi, either via HDMI + keyboard, SSH or Serial
-   Copy the `piemucd.py` to the home folder of your user
-   Add `sudo python3 ~/piemucd.py` to the end of `~/.profile` to have the script start up on login
-   Set up the user to automatically login on startup using `sudo raspi-config`

3. Main interface

-   When PiEmuCD is run, it automatically starts up in CD emulation mode. If no `to-be-mounted.txt` file is present on the root of the image store partition, the operation will fail.
-   PiEmuCD has it's own command interface with few commands supported. Type `help` to get a list of all available commands.
-   `switch` will switch modes, `switch cdrom` will switch to CD-ROM emulation mode and `switch store` will switch to the image store being mounted on the virtual USB drive.

4. "To be mounted" file

-   The `to-be-mounted.txt` file specified which of the images on the image store should be mounted in CD-ROM emulation mode.
-   A sample file is provided in the repository.
