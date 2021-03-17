ubuntu@ubuntu:/etc/apt$ lsusb
Bus 001 Device 002: ID 0bda:8179 Realtek Semiconductor Corp.
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 002 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 003 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 004 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub

Is it really a driver issue?
- First of all, one should determine whether the card isn't recognized and/or if it's a radio kill switch preventing it from working. 
- Follow all steps below, as your problem may be two- or three-fold:
```
  $ sudo apt-get update
  $ sudo apt-get install lshw
  $ sudo lshw -C network 
  
```
- In case multiple devices are listed, locate the device concerned.
- In case it's listed as *-network UNCLAIMED, 
- you should follow the steps in Installing (newer) drivers.
- In case it's listed as *-network (without 'Unclaimed'), 
- the output below about the driver could be relevant in further steps, 
- e.g. configuration: broadcast=yes driver=iwlwifi


- In case your device isn't listed at all, try the additional steps in Identifying the exact hardware.
- Run tool for enabling and disabling wireless devices. 
``` 
    $ rfkill list 
```
- This lists the state of radio killswitches. Sample output:

1: phy0: Wireless LAN
        Soft blocked: no
        Hard blocked: no
        
- In case you see yes on Hard blocked: 
    - refer to your notebook manual for a hardware switch for Wireless LAN.
- In case you see yes on Soft blocked: 
    - hotkeys on your notebook may help activating it, 
    - as well as hitting "Enable Wireless" in the Network Manager applet. 
- If that fails to remove the soft block, run 
```
  $ sudo rfkill unblock all
```
In case you don't see any kill switches listed: this might not apply for your device. Usually only mobile PCs are equipped with killswitches.
Only for USB devices: exclude USB-level issues.

Preferably, try one directly attached to your mainbord, avoiding hubs or your computer case's connectors.
Try using another type of USB port (e.g. USB2.0 instead of USB3.0 port).
Go to Identifying the exact hardware and see if you can see some error messages when you plug in your device.
Try another cable (if any) you've verified is working.
