# pi-top-setup

This repository includes information and programs to use Raspbian Stretch on the pi-top laptop
(version 1 and 2) and the pi-topCEED.

The help of @pi-top and especially @m-roberts to get this to work is very much appreciated.

The pi-top Device Manager, which handles the pi-top hardware (hub) and the pi-top accessories
(pi-topSPEAKER and pi-topPULSE) is now available for Raspbian Stretch. This is the recommended
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
pi-topPULSE. It can also be installed with the following commands:
 
```
  sudo apt update
  sudo apt upgrade
  sudo apt install pt-hub
  sudo systemctl disable pt-display
```
If you want to understand the consequences of the last line above (disable pt-display),
see issue #2 in this repository.

If you are installing this software on a pi-top rev 1 or pi-topCEED, make sure that spi
is enabled in menu->Preferences->Raspberry Pi Configuration.

Once the software is installed, you can obtain information from the pi-top hardware, and change
certain parameters:


**Battery**

>Starting with the latest upgrade of Raspian Stretch (December 1, 2017) a battery icon
>should be automatically installed and enabled on the pi-top rev 1.
>The apt package *lxplug-ptbatt* is part of the apt package *raspberry-pi-ui-mods*.
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

If you prefer to see a battery icon with the current charge of the battery in the
system tray section of the desktop panel, you can install
[pi-top-battery-widget](http:github.com/rricharz/pi-top-battery-widget)


**Screen**

On the pi-top version 2 the brightness keys work with out-of-the-box Raspbian Stretch.
On the pi-top version 1 see *Enable the brightness keys* below.

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
menu->Preferences->pi-top Configuration. I recommend to keep pi-top-setup in
Downloads. This makes future upgrading or uninstalling easier.

![Alt text](config.png?raw=true "menu item")


**Additional tools to debug problems with the device manager**

If you install pi-top Configuration (instructions above), the following additional
tools are also installed: 

*pt-log* displays the log of pt-device-manager (current session).

*pt-devices* displays the current host device and peripherals handled by
pt-device-manager.

*audiotest* plays a short sound on the speaker.

Example output of *pt-devices*:
```
  pi@pitop:~ $ pt-devices
  Devices and peripherals handled by pt-device-manager:
  OS release: 4.9.59-v7+
  Host device is pi-top v1
  Peripheral pi-topSPEAKER-v1-mono is currently enabled
  pi@pitop:~ $
```


**Enable the brightness keys on the pi-top (version 1) keyboard**

Thanks to @m-roberts and @o355 for help to get this to work.

The recommended way to enable the brightness keys is to install pt-input.
The advantage of using pt-input is that the brightness keys also work when using
the command line interface and not only on the desktop. Unfortunately,
pt-input does not work properly on Raspbian Stretch as present, but a fix is
described below

To install pt-input, open a terminal and type

```
  sudo apt update
  sudo apt install pt-input
```

Wait a few seconds and then check whether the brightness keys work.


**What to do if the brightness keys on the pi-top (version 1) still do not work**

If you have not yet installed the Device Manager, proceed as described at the
top of this page. If you have already installed the Device Manager, pt-brightness
works, pt-input has been installed and the brightness keys still do not work,
you have to fix pt-brightness to work properly on Raspbian Stretch:

Download this repository if you have not already done so:

```
  cd
  cd Downloads
  git clone --depth 1 git://github.com/rricharz/pi-top-setup
```

Go into the downloaded folder and execute fix-pt-input:
```
  cd
  cd Downloads
  cd pi-top-setup
  chmod +x fix-pt-input
  ./fix-pt-input
```

Important: fix-pt-input might take several minutes to execute.
Do not interrupt it during the installation!

Experienced users can also modify any key on the keyboard by modifying the
file /etc/pi-top/pt-input/keyboard-commands. As @o355 pointed out, one can
boot the pi-top in the command line interface (cli) and then use showkey to
get the proper keycode for any key on the keyboard.


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


Please open an issue in this repository or write to rricharz77@gmail.com if you have any feedback
or problem with this repository. Your input is appreciated.
