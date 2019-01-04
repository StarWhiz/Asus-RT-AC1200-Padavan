# Asus-RT-AC1200-Padavan

ASUS RT-AC1200 Router Firmware

This is custom firmware (Padavan) that has been built for the Asus RT-AC1200 Dual band AC Router.

It's been built with some modifications to the base config from: https://bitbucket.org/padavan/rt-n56u/src/32a93db4026cc2cff585d7008373432d888fc1aa/trunk/configs/templates/ac1200hp_base.config?at=master&fileviewer=file-view-default

Modifications to build:
CONFIG_FIRMWARE_INCLUDE_OPENVPN=n
CONFIG_FIRMWARE_INCLUDE_QOS=y

OPENVPN was not included because it caused the build to fail.
QOS was included for Smart Queue Management with fq_codel

fq_codel must be configured by your own script (via 'tc' utility).
The webUI does not support QoS/Shaper. (Source: https://bitbucket.org/padavan/rt-n56u/issues/170/smart-queue-management)


*These instructions written below were based off the RT-N600 readme.md from https://github.com/russinnes/RT-N600-Padavan by russinnes

Trying to update the stock firmware through the ASUS web GUI will NOT WORK! For the initial upgrade from the stock firmware:

###Instructions:###
1) Download RT-AC1200_3.4.3.9-099 from this repository
2) -Download the Asus recovery firmware (windows) tool from http://dlcdnet.asus.com/pub/ASUS/LiveUpdate/Release/Wireless/Rescue.zip
   -Also works on a Windows VM with a bridged network adapter to the ethernet port with a manual IP
   -Set your ethernet IP manually 192.168.1.5 / 255.255.255.0 with NO gateway
   
4) Plug in your ethernet to LAN port 1 on the router

5) Load up the recovery software with the RT-AC1200_3.4.3.9-099 firmware file, but don't press "Upload" yet.

6) Plug in the router to power WHILE HOLDING the reset button in. While CONTINUING to hold the button, select "Upload"
   Continue to hold the reset button in until it finishes and verifies!
   
6b) If that doesn't work try pressing "Upload" first just before you do step 6. At some point while holding reset the rescue tool will finally detect and upload the firmware. That's when you can let go of the reset button.
   
7) The router will reboot and not much will happen. Wait a minute or 2. 

8) Power off and on the router again. Voila. Set everything your Ethernet IP back to DHCP (automatically) and you're good to go. 

9) L:admin P:admin

 

  
