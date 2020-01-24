# Realtek 8192eu for CentOS(8.0.1905) for Linux 4.18.0 Kernel

[![License: GPL v3](https://img.shields.io/badge/License-GPL%20v3-blue.svg)](http://www.gnu.org/licenses/gpl-3.0)
[![master](https://img.shields.io/badge/current-v5.2.19.2-aa11ff.svg)](https://github.com/noud/rtl8192EU_WiFi_linux/releases)

## How to build:

```sh
  $ sudo su
  # make clean
  # make -j4
  # make strip
  # modprobe mac80211
  # modprobe cfg80211
  # insmod 8192eu.ko
  # cp 8192eu.ko /lib/modules/`uname -r`/kernel/drivers/net/wireless
  # depmod -a
```
## Add blacklist:

  vim /etc/modprobe.d/blacklist.conf 
  
 add:
 
  blacklist rtl8xxxu
  
## Add wifi reconnect script 192.168.0.1(route address)
```
vim /home/wificheck.sh

#!/bin/bash

timeout 1 ping 192.168.0.1 -c 1 2>/dev/null 1>&2
if [ $? != 0 ]; then
nmcli radio wifi off && sleep 1 && nmcli radio wifi on
fi
```
## Crontab Task every minute

```
crontab -e (Type Enter button)

* * * * * /home/wificheck.sh
```
## service crond reload

## reboot

## modinfo 8192eu
```
filename:       /lib/modules/4.18.0-80.11.2.el8_0.x86_64/kernel/drivers/net/wireless/8192eu.ko
version:        v5.6.4_35685.20191108_COEX20171113-0047
author:         Realtek Semiconductor Corp.
description:    Realtek Wireless Lan Driver
license:        GPL
rhelversion:    8.0
srcversion:     4FE8DF2867DB4639070C444
alias:          usb:v2C4Ep0104d*dc*dsc*dp*ic*isc*ip*in*
alias:          usb:v2C4Ep0100d*dc*dsc*dp*ic*isc*ip*in*
alias:          usb:v2001p3319d*dc*dsc*dp*ic*isc*ip*in*
alias:          usb:v2019pAB33d*dc*dsc*dp*ic*isc*ip*in*
alias:          usb:v2357p0126d*dc*dsc*dp*ic*isc*ip*in*
alias:          usb:v2357p0109d*dc*dsc*dp*ic*isc*ip*in*
alias:          usb:v2357p0108d*dc*dsc*dp*ic*isc*ip*in*
alias:          usb:v2357p0107d*dc*dsc*dp*ic*isc*ip*in*
alias:          usb:v0BDAp818Cd*dc*dsc*dp*icFFiscFFipFFin*
alias:          usb:v0BDAp818Bd*dc*dsc*dp*icFFiscFFipFFin*
depends:        cfg80211
name:           8192eu
vermagic:       4.18.0-80.11.2.el8_0.x86_64 SMP mod_unload modversions 
```
