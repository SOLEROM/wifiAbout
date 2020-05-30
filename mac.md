# mac

## ref
* https://blog.quarkslab.com/reverse-engineering-broadcom-wireless-chipsets.html

## about
* The MAC layer uses three types of frames: management, data and control
* Management frames are managed by an entity called MLME (MAC subLayer Management Entity)
* the location of the core that processes MLME define the mac type

## mac types

### softmac
* the MLME is running in the kernel driver

### fullMAC
* also called hardMac
* MLME is in the firmware, embedded in the chip
* FullMAC devices offer better performance in terms of power consumption and speed
* are heavily used in smartphones and tend to be the most used kind of chips
* limit ability of the users to send specific frames
* to set them in monitor mode one will need to edit directly the firmware running on the chips


### hybrid
* some hybrid implementations of soft hard mac
* for example, probe responses and requests are managed by the driver, but association requests and authentication are dealt by the chip's firmware.

## linux perspective
* in SoftMAC device, the kernel will use a specific Linux Kernel Module (LKM) called 'mac80211'
* This driver exposes the MLME API in order to manage the Management frames
* otherwise the kernel will use directly a hardware driver and offload MLME processing to the chip's firmware.

![](../media/01.png)

* All new Linux wireless drivers should be written targeting either cfg80211 for fullmac devices or mac80211 for softmac devices

