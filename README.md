# pi-topPULSE

![Image of <b>pi-top</b>PULSE addon board](https://static.pi-top.com/images/pulse-small.png "Image of pi-topPULSE addon board")

Visit the [<b>pi-top</b>PULSE product page](https://pi-top.com/products/pulse) on the <b>pi-top</b> website for more information.

## Table of Contents
* [Quick Start](#quick-start)
* [Hardware Overview](#hardware)
* [Software](#software)
    * [<b>pi-top</b>PULSE on <b>pi-top</b>OS](#software-pt-os)
    * [<b>pi-top</b>PULSE on Raspbian](#software-raspbian)
    * [How it works - 'under the hood'](#software-how-it-works)
* [Using <b>pi-top</b>PULSE](#using)
	* [Amazon's Alexa Voice Service](#using-avs)
	* [Using a custom Python script](#using-script)
* [Documentation & Support](#support)
	* [Links](#support-links)
	* [Troubleshooting](#support-troubleshooting)

## <a name="quick-start"></a> Quick Start
### pi-topPULSE on pi-topOS
* Boot into <b>pi-top</b>OS (released on or after 12-07-2017)
* Plug in <b>pi-top</b>PULSE
* Follow on-screen instructions, if necessary
* Enjoy - check out the [examples](https://github.com/pi-top/pi-topPULSE/tree/master/examples) to see what you can do! And try asking Alexa questions via <b>pi-top</b>DASHBOARD!

### pi-topPULSE on Raspbian
* Run the following commands in the terminal (with an internet connection):

```
sudo apt update
sudo apt install pt-pulse
```

* Plug in <b>pi-top</b>PULSE
* Follow on-screen instructions, if necessary
* Enjoy - check out the [examples](https://github.com/pi-top/pi-topPULSE/tree/master/examples) to see what you can do! See [here](https://github.com/pi-top/Alexa-Voice-Service-Integration) for more on using <b>pi-top</b>'s Alexa Voice Service integration.

## <a name="hardware"></a> Hardware Overview

<b>pi-top</b>PULSE is a 7x7 LED array, a speaker and a microphone. Additionally the device features ambient lights which reflect the state of the LED array, 4 around the speaker, and 3 on the underside. <b>pi-top</b>PULSE uses a variety of interfaces to communicate with the Raspberry Pi: the speaker uses I2S, and the LEDs and microphone use serial (UART) - Tx and Rx respectively. <b>pi-top</b>PULSE can be used either as a HAT or as <b>pi-top</b> addon.

For information on the pi-topPULSE's GPIO pinout, see [here](https://pinout.xyz/pinout/pi_toppulse).

## <a name="software"></a> Software
### <a name="software-pt-os"></a> pi-topPULSE on pi-topOS

All <b>pi-top</b>PULSE software and libraries are included and configured 'out-of-the-box' as standard on <b>pi-top</b>OS (released on or after 12-07-2017). Simply connect a <b>pi-top</b>PULSE to your <b>pi-top</b>, reboot if instructed to do so, and it will be automatically initialised and ready to produce light, capture and play audio. Volume control is handled by the operating system.

Download the latest version of <b>pi-top</b>OS [here](https://pi-top.com/products/os#download).

As mentioned in the [Hardware Overview](#hardware), the speaker on the <b>pi-top</b>PULSE uses I2S. This requires some configuration, which will require a reboot from a typical Raspbian configuration using the default sound drivers. This is also true in reverse - if you have configured a <b>pi-top</b>PULSE and you wish to use the standard HDMI or 3.5mm sound outputs, you will require a reboot.

#### Additional information
Automatic initialisation is performed by a software package called `pt-peripheral-cfg`. It contains a program called `pt-peripherals-daemon`, which runs in the background and scans for newly connected devices. If a device is detected, and the appropriate library is installed, it will be initialised.

The `pt-pulse` package on <b>pi-top</b>OS installs and starts this background process, as well as the Python library. In the case of <b>pi-top</b>PULSE, it enables I2S and configures UART for next boot, if not currently enabled/configured, and notifies the user if a reboot is required. If a reboot is not required, it will initialise the device.

### <a name="software-raspbian"></a> pi-topPULSE on Raspbian
The <b>pi-top</b>PULSE software exists on the Raspbian software repositories. Simply run the following commands at the terminal (and then reboot):

```
sudo apt update
sudo apt install pt-pulse
```

If you prefer to manually install the packages or want to install a specific set of packages see the [Manual Configuration and Installation](https://github.com/pi-top/pi-topPULSE/wiki/Manual-Configuration-and-Installation) page on the wiki.

### <a name="software-how-it-works"></a> How it works - 'under the hood'
For more information on how to use the library files, take a look at the [initialisation section of the 'Manual Configuration and Installation'](https://github.com/pi-top/pi-topPULSE/wiki/Manual-Configuration-and-Installation#using-the-software-library-to-manually-initialise-pi-toppulse) page on the wiki.
Also check out the [examples](https://github.com/pi-top/pi-topPULSE/tree/master/examples) folder for guidance of what the library is capable of.

## <a name="using"></a> Using <b>pi-top</b>PULSE

### <a name="using-avs"></a> Amazon's Alexa Voice Service

See [here](https://github.com/pi-top/Alexa-Voice-Service-Integration) for more on using <b>pi-top</b>'s Alexa Voice Service integration.

### <a name="using-script"></a> Using a custom Python script

Using the `ptpulse` Python module requires root access to function. If you are running a script, make sure that you are running it with root access. You can do this with the "sudo" command:

	sudo python3 my_cool_pulse_script.py


Alternatively, if you are running Python in `IDLE`, please make sure you start LXTerminal and run idle or idle3 with the "sudo" command, like so:

	sudo idle3

## <a name="support"></a> Documentation & Support
### <a name="support-links"></a> Links
* [GPIO Pinout](https://pinout.xyz/pinout/pi_toppulse)
* [Support](https://support.pi-top.com/)

### <a name="support-troubleshooting"></a> Troubleshooting
#### Why is my pi-topPULSE not working?

* Currently, **<b>pi-top</b>PULSE is only supported on Raspberry Pi 3**. This is due to problems setting the UART clock speed on earlier Raspberry Pi models. It might be possible to get this to work on earlier versions, but this is not currently supported.

#### I have installed pi-topPULSE software manually...
* If you are running Linux kernel version 4.9.x previous to 4.9.35, <b>pi-top</b>PULSE [may not be fully functional](https://github.com/raspberrypi/linux/issues/1855). In particular, this issue prevents the <b>pi-top</b>PULSE LEDs from working. If you are experiencing this issue, please check your kernel version by typing `uname -r` at the terminal. You can update your kernel version to the latest by running `sudo apt install raspberrypi-kernel`.

* If you are attempting to use Python 3, and have installed manually, you need to ensure that you have the latest version of the PySerial module. Take a look at [the script](manual-install/upgrade-python3-pyserial) in the `manual-install` directory for how to do this.

#### The red LED on the underside of my pi-topPULSE is on - what does this mean?
* This LED indicates that the sampling rate of the microphone is set to 16kHz. By default, when plugged in, you will see that this LED is switched on, and can be used as a guide to show that it has not yet been initialised. Once initialised, the default sample rate is 22050Hz (~22KHz), and this is why the red LED is switched off. *Note: [<b>pi-top</b>'s Amazon Alexa Voice Service integration](https://github.com/pi-top/Alexa-Voice-Service-Integration) uses 16kHz, which is denoted with the red LED being on. In this context, the red LED can be considered as an indicator that the <b>pi-top</b>PULSE is capturing audio.*

#### Why can't I get my Bluetooth working after connecting a pi-topPULSE?
* This is a known issue, and we are evaluating the best user experience for resolving this issue. In the meantime, this issue is captured [here](https://github.com/pi-top/pi-topPULSE/issues/4) - follow the instructions to re-enable Bluetooth.
