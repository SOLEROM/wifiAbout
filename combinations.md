# wifi combinations

## AP

```
You need a nl80211 compatible wireless device, which supports the AP operating mode.

$ iw list
=========
Wiphy phy1
...
	Supported interface modes:
		 ....
		 * managed
		 * AP
		 .....

```


## combine

If your hardware and the kernel driver supports a simultaneous STA / AP mode you can stay connected to another access point while running your own.

```
iw list
========

	valid interface combinations:
		 * #{ managed } <= 1, #{ AP, P2P-client, P2P-GO } <= 1, #{ P2P-device } <= 1,
		   total <= 3, #channels <= 2

```

* The notation #{ ... } reads "number of interface of the following type"
* You can have a maximum a 3 simultaneous interfaces
* Those interfaces can use at most 2 different channels 
* so at least 2 interfaces must use the same channel
* You can have one managed interface (also called "station" or "client")
* either one access point (AP) or one P2P-client or one P2P-GO interface
* and one P2P-device interface.


* The primary use-case is to support simultaneous operation as a station on one channel and as an access-point on a different channel
* Simultaneous operation on two channels in the same band (2.4GHz or 5GHz)


## example2

```
valid interface combinations:
         * #{ managed } <= 1, #{ AP } <= 1,
           total <= 2, #channels <= 1, STA/AP BI must match
         * #{ managed } <= 2,
           total <= 2, #channels <= 1

```

* BI is the beacon interval

```
kernel source in include/net/cfg80211.h:
struct ieee80211_iface_combination:
===================================
 * @beacon_int_infra_match: In this combination, the beacon intervals
 *  between infrastructure and AP types must match. This is required
 *  only in special cases.

```

```
#channels <= 1 :
================
use only one channel when I have two vif's on the same physical device
means that your software AP must operate on the same channel as your Wi-Fi client connection;
```


