
## exmaple #1

hw

```
lspci
=====
01:00.0 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL8111/8168/8411 PCI Express Gigabit Ethernet Controller (rev 15)

lspci -vv -s 01:00.0
=====================
01:00.0 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL8111/8168/8411 PCI Express Gigabit Ethernet Controller (rev 15)
	Subsystem: Dell RTL8111/8168/8411 PCI Express Gigabit Ethernet Controller
	Control: I/O+ Mem+ BusMaster+ SpecCycle- MemWINV- VGASnoop- ParErr- Stepping- SERR- FastB2B- DisINTx+
	Status: Cap+ 66MHz- UDF- FastB2B- ParErr- DEVSEL=fast >TAbort- <TAbort- <MAbort- >SERR- <PERR- INTx-
	Latency: 0, Cache Line Size: 64 bytes
	Interrupt: pin A routed to IRQ 16
	Region 0: I/O ports at 3000 [size=256]
	Region 2: Memory at a1204000 (64-bit, non-prefetchable) [size=4K]
	Region 4: Memory at a1200000 (64-bit, non-prefetchable) [size=16K]
	Capabilities: <access denied>
	Kernel driver in use: r8169
	Kernel modules: r8169


```

rev

```
lspci -n -s 01:00.0
01:00.0 0200: 10ec:8168 (rev 15)
solov@vostro14:/data/todo$ lspci -nn -s 01:00.0
01:00.0 Ethernet controller [0200]: Realtek Semiconductor Co., Ltd. RTL8111/8168/8411 PCI Express Gigabit Ethernet Controller [10ec:8168] (rev 15)

```

lshw

```
sudo lshw -C network
[sudo] password for solov: 
  *-network
       description: Ethernet interface
       product: RTL8111/8168/8411 PCI Express Gigabit Ethernet Controller
       vendor: Realtek Semiconductor Co., Ltd.
       physical id: 0
       bus info: pci@0000:01:00.0
       logical name: enp1s0
       version: 15
       serial: 6c:2b:59:6c:60:77
       capacity: 1Gbit/s
       width: 64 bits
       clock: 33MHz
       capabilities: pm msi pciexpress msix bus_master cap_list ethernet physical tp mii 10bt 10bt-fd 100bt 100bt-fd 1000bt-fd autonegotiation
       configuration: autonegotiation=on broadcast=yes driver=r8169 firmware=rtl8168h-2_0.0.2 02/26/15 latency=0 link=no multicast=yes port=MII
       resources: irq:16 ioport:3000(size=256) memory:a1204000-a1204fff memory:a1200000-a1203fff

```

driver

```
lsmod |grep r8169
r8169                  81920  0

lsmod | grep -i wifi
iwlwifi               348160  1 iwlmvm
cfg80211              704512  3 iwlmvm,iwlwifi,mac80211

```


```
modinfo r8169
==============
filename:       /lib/modules/5.3.0-51-generic/kernel/drivers/net/ethernet/realtek/r8169.ko
firmware:       rtl_nic/rtl8107e-2.fw
firmware:       rtl_nic/rtl8107e-1.fw
firmware:       rtl_nic/rtl8168h-2.fw
firmware:       rtl_nic/rtl8168h-1.fw
firmware:       rtl_nic/rtl8168g-3.fw
firmware:       rtl_nic/rtl8168g-2.fw
firmware:       rtl_nic/rtl8106e-2.fw
firmware:       rtl_nic/rtl8106e-1.fw
firmware:       rtl_nic/rtl8411-2.fw
firmware:       rtl_nic/rtl8411-1.fw
firmware:       rtl_nic/rtl8402-1.fw
firmware:       rtl_nic/rtl8168f-2.fw
firmware:       rtl_nic/rtl8168f-1.fw
firmware:       rtl_nic/rtl8105e-1.fw
firmware:       rtl_nic/rtl8168e-3.fw
firmware:       rtl_nic/rtl8168e-2.fw
firmware:       rtl_nic/rtl8168e-1.fw
firmware:       rtl_nic/rtl8168d-2.fw
firmware:       rtl_nic/rtl8168d-1.fw
license:        GPL
softdep:        pre: realtek
description:    RealTek RTL-8169 Gigabit Ethernet driver
author:         Realtek and the Linux r8169 crew <netdev@vger.kernel.org>
srcversion:     7708157E7E729C0D41B09C8
alias:          pci:v00000001d00008168sv*sd00002410bc*sc*i*
alias:          pci:v00001737d00001032sv*sd00000024bc*sc*i*
alias:          pci:v000016ECd00000116sv*sd*bc*sc*i*
alias:          pci:v00001259d0000C107sv*sd*bc*sc*i*
alias:          pci:v00001186d00004302sv*sd*bc*sc*i*
alias:          pci:v00001186d00004300sv*sd*bc*sc*i*
alias:          pci:v00001186d00004300sv00001186sd00004B10bc*sc*i*
alias:          pci:v000010ECd00008169sv*sd*bc*sc*i*
alias:          pci:v000010FFd00008168sv*sd*bc*sc*i*
alias:          pci:v000010ECd00008168sv*sd*bc*sc*i*
alias:          pci:v000010ECd00008167sv*sd*bc*sc*i*
alias:          pci:v000010ECd00008161sv*sd*bc*sc*i*
alias:          pci:v000010ECd00008136sv*sd*bc*sc*i*
alias:          pci:v000010ECd00008129sv*sd*bc*sc*i*
alias:          pci:v000010ECd00002600sv*sd*bc*sc*i*
alias:          pci:v000010ECd00002502sv*sd*bc*sc*i*
depends:        
retpoline:      Y
intree:         Y
name:           r8169
vermagic:       5.3.0-51-generic SMP mod_unload 
signat:         PKCS#7
signer:         
sig_key:        
sig_hashalgo:   md4
parm:           debug:Debug verbosity level (0=none, ..., 16=all) (int)

```

FW

```
/lib/firmware/rtl_nic/
======================
rtl8105e-1.fw  rtl8107e-1.fw  rtl8168d-2.fw  rtl8168e-3.fw  rtl8168g-1.fw  rtl8168h-1.fw  rtl8411-1.fw
rtl8106e-1.fw  rtl8107e-2.fw  rtl8168e-1.fw  rtl8168f-1.fw  rtl8168g-2.fw  rtl8168h-2.fw  rtl8411-2.fw
rtl8106e-2.fw  rtl8168d-1.fw  rtl8168e-2.fw  rtl8168f-2.fw  rtl8168g-3.fw  rtl8402-1.fw

```


## drivers

r8169              
iwlwifi
iwlmvm
cfg80211  
mac80211



