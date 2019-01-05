# Asus-RT-AC1200-Padavan

ASUS RT-AC1200 Router Firmware

This is custom firmware (by Padavan) that has been built for the Asus RT-AC1200 Dual band AC Router.

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

 
## Enabling fq_codel on startup ##

* Navigate to Advanced Settings > Administration > Settings
* Then under NVRAM to Flash Meory Committing Mode: Choose "Manual Only"
* Navigate to Advanced Settings > Customization > Scripts > Run After Router Started:
* Then add the following line to the bottom of the script

> IF=eth2

> tc qdisc del dev $IF root

> tc qdisc add dev $IF root handle 1: htb

> tc class add dev $IF parent 1: classid 1:1 htb rate 3800kbps

> tc qdisc add dev $IF parent 1:1 handle 10: fq_codel

> tc filter add dev $IF protocol ip prio 1 u32 match ip dst 0.0.0.0/0 flowid 1:1

* After that press "Commit" near the logout buttom.
* When prompted, answer "Yes" to commit from NVMRAM to Flash.

eth2 is my WAN interface in this example. yours might be different. you can check which interface is your wan by typing "ifconfig" when you ssh or telnet into the router.

3800kbps was about 90% of my actual upload speed of 4200kbps.
  
