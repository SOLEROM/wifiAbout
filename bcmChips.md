# bcm chips

* use an ARM Cortex-M3 or an ARM Cortex-R4 as the main MCU for non-time-critical operations
* deal with two similar instruction sets: armv7m and armv7r.
* These MCUs have one ROM and one RAM
* All time-critical operations are realised by a Broadcom proprietary processor called D11 core, mostly responsible of the PHY layer.

## Firmwares
* split in two parts: one part is written into the ROM and cannot be modified, the other part is uploaded by the driver into the chip's RAM.
* By doing so the vendor is able to add new features or write updates for their chips, just by changing the RAM portion of the firmware.

![](../media/02.png)

* Open source:

```
    b43 (reversed from proprietary wl / old SoftMAC / Linux)
    brcmsmac (SoftMAC / Linux)
    brcmfmac (FullMAC / Linux)
    bcmdhd ( FullMAC / Android)
```

* Proprietary:

```
    broadcom-sta aka 'wl' ( SoftMAC && FullMAC / Linux)

!!! the wl driver uses it's own MLME and doesn't need the LKM 'mac80211' to process Management frame !!!
```




