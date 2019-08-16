# pi-top-setup

This repository includes information and programs to use Raspbian Buster and Raspbian Stretch on the pi-top laptop
and the pi-topCEED (pi-top [1], pi-top [2] and pi-top [3]).

The help of @pi-top and especially @m-roberts to get this to work is very much appreciated.

The pi-top Device Manager, which handles the pi-top hardware (hub) and the pi-top accessories
(pi-topSPEAKER and pi-topPULSE) is available for Raspbian Buster and Raspbian Stretch. This is the recommended
way to use the pi-top with Raspbian. The documentation can be found at the
[pi-top repository](http:github.com/pi-top). You can also find instructions there on how to install
the pi-topSPEAKER, pi-topPULSE and Alexa service. The pi-top Device Manager
also supports pushing the power button for a second as a means to turn the pi-top off.

> **Important!**
> If you have used
> [pi-top-install](http:github.com/rricharz/pi-top-install) or
> [pi-top-battery-status](http:github.com/rricharz/pi-top-battery-status),
> they should not be used together with the
> Device manager. See the instructions for uninstalling them at the links above.

The pi-top Device Manager is automatically installed with the latest software for the pi-topSPEAKER or
pi-topPULSE. It can also be installed with the following commands.
 
```
  sudo apt-get update
  sudo apt-get upgrade
  sudo apt-get install pt-device-manager
```

With the latest release of the pt-device-manager software, it is also possible to install
the software using Raspbian Lite, even so this is not recommended.
**If you are using Raspbian Lite, do not turn off or
reboot your pi-top after installing the pt-device-manager! Instead, type 'sudo raspi-config'
then use 'boot options' and 'Desktop/CLI' to set your bootup to Console.** Afterwards, you
can reboot your pi-top.

If you are installing this software on a pi-top [1] or pi-topCEED, make sure that spi
is enabled in menu->Preferences->Raspberry Pi Configuration.

Once the software is installed, you can obtain information from the pi-top hardware, and change
certain parameters:


**Battery**

>A battery icon
>should be automatically installed and enabled on the pi-top laptop (both versions).
>The apt package *lxplug-ptbatt* is part of the apt package *raspberry-pi-ui-mods*.
>If this battery icon shows up on your pi-top, installation of a separate battery widget
>is not required. It will only show up if pt-device-manager is installed
>and i2c is enabled.

>If this battery icon does not show up on your pi-top, you can use the following means to
>display battery information.

The information about the state of the battery can be obtained with the command

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

If you do not see a battery icon on the desktop panel after the next bootup, proceed as follows:
Right click at an empty spot on the desktop panel, and choose "add/remove panel items". Click on
Battery (pi-top/laptop) and click "add". Now you can move the battery icon to your preferred
position with "Up" and "Down", then close the Panel Preferences window. The battery icon only
shows up if pt-device-manager has been installed and works properly.


**Screen**

On the pi-top [2] the brightness keys work with out-of-the-box Raspbian Buster and Raspbian Stretch.

You can control the screen brightness and the timeout before the screen blanks also with
the command pt-brightness. To get information on how to use pt-brightness, type

```
  pt-brightness -h
``` 

If you prefer to adjust brightness and screen blanking using sliders and buttons using
the Raspberry Pi Desktop, you can install pi-top Configuration from this repository as follows

```
  cd
  cd Downloads
  git clone --depth 1 git://github.com/rricharz/pi-top-setup
  cd pi-top-setup
  chmod +x install
  ./install 
```

After installing this program, the sliders and buttons are available using
menu->Preferences->pi-top Configuration. I recommend to keep pi-top-setup in
Downloads. This makes future upgrading or uninstalling easier.

![Alt text](config.png?raw=true "menu item")


**Additional tools**

If you install pi-top Configuration (instructions above), the following additional
tools are also installed: 

*pt-log* displays the log of pt-device-manager (current session).

*pt-devices* displays the current host device and peripherals handled by
pt-device-manager.

*audiotest* plays a short sound on the speaker.

The following command allows to turn the internal touchpad of the pi-top
version 2 off until the next boot, if you are using an external mouse, and are
bothered by unwanted mouse actions.

*touchpad off* turns it off until the next boot

*touchpad on* turns it back on without a new boot

Example output of *pt-devices*:
```
  pi@pitop:~ $ pt-devices
  Devices and peripherals handled by pt-device-manager:
  OS release: 4.9.59-v7+
  Host device is pi-top v1
  Peripheral pi-topSPEAKER-v1-mono is currently enabled
  pi@pitop:~ $
```

**To update pi-top Configuration to the latest version**

Open a terminal and type

```
  cd
  cd Downloads/pi-top-setup
  git pull
  ./install
```


**To uninstall pi-top Configuration**

Open a terminal and type

```
  cd
  cd Downloads/pi-top-setup
  chmod +x uninstall
  ./uninstall
```


**Additional documents describing how to use your pi-top**

[Using the analogue inputs of the pi-topPROTO+ with python](http:github.com/rricharz/pi-top-setup/blob/master/documents/ProtoPlus.pdf)

[Problems with an attached USB stick](http:github.com/rricharz/pi-top-setup/blob/master/documents/use_of_usb_stick.txt)



**What to do if bluetooth does not work after installing pt-pulse**

See the workaround at the bottom of [pi-topPULSE](https://github.com/pi-top/pi-topPULSE).


**How to upgrade pt-device-manager if you had installed earlier versions of pt-hub**

First, uninstall the existing pt-device-manager software (earlier than May 18, 2018)
with the following commands:
```
  sudo apt-get update
  sudo apt-get purge pt-hub pt-device-manager
  sudo apt-get autoremove
```

Do not reboot right now, but install the latest version:
```
  sudo apt-get install pt-device-manager
  sudo apt-get upgrade
```

Now you can reboot your pi-top.


**Links to other contributions for the pi-top**

Mike Spivey has adapten a script that's automatically invoked by udev rules and disables the touchpad automatically,
if an external mouse is plugged in, and enabling it again if the mouse is umplugged.
See http://spivey.oriel.ox.ac.uk/corner/Touchpad_control_for_pi-top


Please open an issue in this repository or write to rricharz77@gmail.com if you have any feedback
or problem with this repository. Your input is appreciated.
