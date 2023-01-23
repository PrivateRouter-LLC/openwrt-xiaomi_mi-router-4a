# Xiaomi Mi Router 4A Gigabit Edition: PrivateRouter OpenWRT with V2rayA

*After first flash connect internet to download drivers and V2rayA*

Warning: This router is not same as the Mi Router 4A 100m, please don't brick your router :)

Important notes:

03/2022 -  OpenWrt will not work on units with the Eon or CFeon flash chips at this time. There are no reported issues with Winbond or GigaDevice flash chips fitted to earlier manufactured units. Other differences have also been observed with chinese model made in Sept 2021:
https://forum.openwrt.org/t/observations-on-xiaomi-mir4ag-newer-firmware/127373

10/2022 - Xiaomi is currently shipping v2 of the 4A Gigabit Edition, it's identifiable by fw version 2.30.20, and the name when assigned an IP from a DHCP (not your ISPs) via the WAN port, MiWiFi-R4AV2. This model cannot be flashed with Openwrt:
https://forum.openwrt.org/t/support-for-xiaomi-router-ac1200-rb02/124962

How to Install PrivateRouter OpenWRT:

For installing OpenWrt there are the following methods:

1. Using a firmware exploit

Directions can be found at the OpenWRTInvasion repository:
https://github.com/acecilia/OpenWRTInvasion

How to flash Video: https://www.youtube.com/watch?v=SLbkce-M2nE

2. Using a chip programmer (Requires extra hardware to read the stock firmware directly from the SPI flash chip)

Directions can be found on the OpenWRT forums:
https://forum.openwrt.org/t/xiaomi-mi-router-4a-gigabit-edition-r4ag-r4a-gigabit-fully-supported-but-requires-overwriting-spi-flash-with-programmer/36685

# Notes on firmware exploit procedure using Linux

To get stock

- Reset router if necessary to restore default settings.
- Connect computer to ethernet LAN port.
- Connect xiaomi router to the internet with the wan port
- Enter 192.168.31.1
- Configure device, select language, accept terms
- Enter a wifi password (that is the admin password)
- Go to 192.168.31.1 and enter the root password
- When you are in, your link changed and now it have a part with something similar to stok=3700b146c87e45fea51170f87f47d34c
- On terminal enter: git clone https://github.com/acecilia/OpenWRTInvasion
- On terminal enter: cd OpenWRTInvasion
- On terminal enter: python3 remote_command_execution_vulnerability.py , and put the ip and stok, it should work

[download your openwrt image, use squashfs-sysupgrade.bin image]

- start ftp session with user root and password root
- ftp 192.168.31.1
- cd tmp
- put path/to/openwrt-firmware.bin
- telnet session with user root and password root
- telnet 192.168.31.1
- cd /tmp
- mtd -e OS1 -r write openwrt.bin OS1

Warning: If you got the below error message when trying to write the openwrt image with mtd command

Could not open mtd device: OS1
Can't open device for writing! 

You can run cat /proc/mtd to check the flash layout. In this case, your router is having a different flash layout and you should not proceed with the installation using mtd.

# Installation procedure using Microsoft Windows

If you are unable to use a linux computer, there is an alternative to use Microsoft Windows 10 utilising the same exploit, to install OpenWrt onto 4A Gigabit router. Link to Instructions and tools:
https://www.dropbox.com/sh/d3alxc4hi9hb2g6/AABqBbPWrVdJ3XE5SaGqh8AWa?dl=0

# Installation

OpenWrt Factory Firmware: Use this file the first time you flash OpenWrt onto the router going from stock to OpenWRT.
OpenWrt Sysupgrade Firmware: Use this file to upgrade an OpenWrt “system” to a newer OpenWrt version.
OEM Stock Firmware: The above mentioned exploit provides a stock firmware image in its repository.

# Debricking:

Mi Wifi Repair tool:
https://forum.openwrt.org/t/xiaomi-mi-router-4a-gigabit-edition-r4ag-r4a-gigabit-fully-supported-and-flashable-with-openwrtinvasion/36685/747

Zorro Router debrick method:
https://forum.openwrt.org/t/xiaomi-mi-router-4a-gigabit-edition-r4ag-r4a-gigabit-fully-supported-but-requires-overwriting-spi-flash-with-programmer/36685/678
