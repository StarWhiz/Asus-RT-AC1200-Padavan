# Asus-RT-AC1200-Padavan

ASUS RT-AC1200 Router Firmware

This is custom firmware (by Padavan) that has been built for the Asus RT-AC1200 Dual band AC Router.

Wifi 2.4G/5G work. Basic out of the box functions appear to work as well...

It's been built with some modifications to the base config from: https://bitbucket.org/padavan/rt-n56u/src/32a93db4026cc2cff585d7008373432d888fc1aa/trunk/configs/templates/ac1200hp_base.config?at=master&fileviewer=file-view-default

## Modifications to build:

CONFIG_FIRMWARE_INCLUDE_OPENVPN=n

CONFIG_FIRMWARE_INCLUDE_QOS=y

OPENVPN was not included because it caused the build to fail.

QOS was included for Smart Queue Management with fq_codel

fq_codel must be configured by your own script (via 'tc' utility).

The webUI does not support QoS/Shaper. (Source: https://bitbucket.org/padavan/rt-n56u/issues/170/smart-queue-management)

I built this version for the purpose of stopping bufferbloat or lag for my fellow gamer friend with this specific router model. You can read more about this on my website at www.stoplagging.com


## Firmware Flashing Instructions ##
Trying to update the stock firmware through the ASUS web GUI will NOT WORK!

*These instructions written below were based off the RT-N600 readme.md from https://github.com/russinnes/RT-N600-Padavan by russinnes

1) Download RT-AC1200_3.4.3.9-099 from this repository
2) Download the Asus recovery firmware (windows) tool from http://dlcdnet.asus.com/pub/ASUS/LiveUpdate/Release/Wireless/Rescue.zip 
3) Set your ethernet IP manually 192.168.1.5 / 255.255.255.0 with NO gateway
3) Plug in your ethernet to LAN port 1 on the router

4) Load up the recovery software with the RT-AC1200_3.4.3.9-099 firmware file, but don't press "Upload" yet.

5) Plug in the router to power WHILE HOLDING the reset button in. While CONTINUING to hold the button, select "Upload"
   Continue to hold the reset button in until it finishes and verifies!
   
6) If that doesn't work try pressing "Upload" first just before you do step 6. At some point while holding reset the rescue tool will finally detect and upload the firmware. That's when you can let go of the reset button.
   
7) The router will reboot and not much will happen. Wait a minute or 2. 

8) Power off and on the router again. Voila. Set everything your Ethernet IP back to DHCP (automatically) and you're good to go. 

9) L:admin P:admin

 
## Enabling fq_codel on startup to stop lag or bufferbloat on online games ##
* NOTE The fq_codel settings don't work yet.... Ignore instructions below for now..
* Navigate to Advanced Settings > Customization > Scripts > Run After Router Started:
* Then copy the lines from the script on this repository: https://github.com/StarWhiz/Asus-RT-AC1200-Padavan/blob/master/fq_codel%20script%20for%20Asus%20AC1200.txt

* After pasting in the script change WAN_UP_SPEED= and WAN_DOWN_SPEED= to be 90% of your max upload speed and 90% of your max download speed. Otherwise fq_codel won't work.
* Finally press "Apply" on the bottom of the web GUI.
* Then navigate to Advanced Settings > Administration > Settings
* Under the "Commit NVRAM Content to Flash Memory Now:" option press the "commit button" to actually save changes.

* eth2 is my WAN interface in this example. yours might be different. you can check which interface is your wan by typing "ifconfig" when you ssh or telnet into the router.

* Congrats now you'll never lag in games again! Check out www.stoplagging.com if you have a different router.
* Credits to : /u/nicefile on reddit for linking me to: http://openrouter.info/forum/viewtopic.php?f=21&t=4605 which helped me make this guide

  
