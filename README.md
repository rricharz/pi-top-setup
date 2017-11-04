# pi-top-setup

This repository includes information and programs to use Raspbian Stretch on th pi-top laptop
(version 1 and 2) and the pi-topCEED.

The pi-top Device Manager, which handles the pi-top hardware (hub) and the pi-top accessories
(pi-topSPEAKER and pi-topPULSE) is now available for Raspbian Stretch. This is the recommended
way to use the pi-top with Raspbian. The documentation is
[here](http:github.com/pi-top).

> **Important!**
> If you have used
> [pi-top-install](http:github.com/rricharz/pi-top-install) or
> [pi-top-battery-status](http:github.com/rricharz/pi-top-battery-status),
> they should not be used together with the
> Device manager. See the instructions for uninstalling them at the links above. 

The pi-top Device Manager is automatically installed with the latest software for the pi-topSPEAKER or
pi-topPULSE. It can also be installed with the following commands:
 
```
  sudo apt update
  sudo apt upgrade
  sudo apt install pt-hub
```
Make sure that spi is enabled in menu->Preferences->Raspberry Pi Configuration

Once the software is installed, you can obtain information from the pi-top hardware, and change
certain parameters:

**Battery**

If you have a pi-top-laptop, the information about the state of the battery can be obtained with
the command

```
  pt-battery
``` 

If the Device Manager has been properly installed, you should get the following output (of course with different values
for each parameter)

```
  Charging State: 0
  Capacity: 70
  Time Remaining: 590
  Wattage: 0
```

If you prefer to see a battery icon with the current charge of the battery in the
system tray section of the desktop panel, you can install
[pi-top-battery-widget](http:github.com/rricharz/pi-top-battery-widget)

**Screen**

You can control the screen brightness and the timeout before the screen blanks with
the command pt-brightness. To get information on how to use pt-brightness, type

```
  pt-brightness -h
``` 

If you prefer to adjust brightness and screen blanking using sliders and buttons, you
can install pi-top Configuration from this repository as follows

```
  cd
  cd Downloads
  git clone --depth 1 git://github.com/rricharz/pi-top-setup
  cd pi-top-setup
  chmod +x install
  ./install 
```

After installing this program, the sliders and buttons are available using
menu->Preferences->pi-topConfiguration