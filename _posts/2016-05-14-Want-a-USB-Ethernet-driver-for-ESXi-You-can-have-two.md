---
title: Want a USB Ethernet driver for ESXi? You can have two.
header:
  teaser: "usb_adapters.png"
category: [Homelab]
tags: [Homelab, ESXi, USB, Ethernet]
---

Ah, that mythical home lab beast: a working USB Ethernet driver for ESXi. You wait and wait for one, and then two come along...

{% include toc %}

## First of all

I would like to acknowledge the help all the people mentioned on this post, knowingly or otherwise, provided me. Their efforts inspired me to try my hand at this.

In particular, I would like to thank William Lam (tip o' the hat to you, Sir), as without his help things would be very different. It was William who provided the solution that allows automatic load of the modules at boot and persistence of the network configuration across reboots. If you have a chance, stop by [virtuallyGhetto](http://www.virtuallyghetto.com) and show you appreciation.

## The story   

If, like myself, you run an ESXi lab based on the Intel NUC, you might have looked at options to add a second Ethernet adapter. For the 3<sup>rd</sup> Generation NUC I solved the problem with my [NUC Squarepants](/Homelab/NUC-Squarepants/) contraption, but was yet to find a good solution for later generations NUCs. That is, until I came across a great post by William Lam called ["Working USB Ethernet Adapter (NIC) for ESXi"](http://www.virtuallyghetto.com/2016/03/working-usb-ethernet-adapter-nic-for-esxi.html).
 
You can read the full details on William's blog, but the gist is that he was trying to resurrect a custom compiled driver that had been posted to the forum at vm-help.com back in 2013. That driver had been successfully compiled and worked fine on ESXi 5.1, but not on 5.5 or 6.0. By the time I came across William's article, he was looking at ways to compile a new version of the driver targeted at later ESXi releases.

My interest was piqued and the question was: could I get it working myself? I decided to have a go, so I spent some time reading the original forum thread to get a feel for what lay ahead. I am by no means a programmer, but I do from time to time write some code. The challenge was set...

The one thing I didn't like about the original driver William had found was the fact that it also needed a modified version of the ```usbnet``` module. I just thought that interfering with the native modules was a step too far, so wanted to avoid that.

Anyway, to cut a long story short, I got the ASIX 88179_178a driver compiled and running on both ESXi 5.5 and 6.0. Funnily enough, by the time I contacted William about my success he had also got the driver built, and both [his](https://github.com/lamw/ax88179_178a-esxi) and [my](https://github.com/gomesjj/ax88179_178a) changes to the Linux source code were pretty much the same. Eventually I also got the driver compiled for ESXi 5.1, which took longer due to a puzzling DMA mask error when connected to USB 2.0 ports. It is resolved now, but bear in mind that the bandwidth limitation on USB 2.0 (there is no support for xHCI on ESXi 5.1) means that the adapter will never achieve Gigabit speeds.

So, that is it? What about the second driver I implied at above? Well, that will be the driver for USB Ethernet adapters based on the Realtek RTL8153/RTL8152 chipset (r8152 driver) that I also got working. You see, once I got the first driver going I got the taste for it and had to have a go at another. The source code for this driver is also on [GitHub](https://github.com/gomesjj/r8152). This second driver also works on ESXi 6.0, 5.5 and 5.1, with the adapter plugged in to either a USB 3.0 or USB 2.0 port (note the bandwidth limitation I mentioned above). Also,  the Realtek driver is slightly faster than the ASIX one.

## Tested devices

The following devices were tested with these drivers.

### ASIX

* [StarTech USB 3.0 to RJ45 Ethernet LAN 10/100/100 Network Adapter](https://www.amazon.co.uk/gp/product/B0095EFXMC/ref=oh_aui_detailpage_o04_s00?ie=UTF8&psc=1)

* [StarTech USB 3.0 to Dual Port Gigabit Ethernet Adapter NIC with USB Port](https://www.amazon.co.uk/gp/product/B00D8XTOD0/ref=oh_aui_detailpage_o03_s00?ie=UTF8&psc=1)

* [Plugable USB 3.0 to 10/100/1000 Gigabit Ethernet LAN Network Adapter](https://www.amazon.co.uk/gp/product/B00AQM8586/ref=oh_aui_detailpage_o02_s00?ie=UTF8&psc=1)

### Realtek

* [ANKER Aluminum USB 3.0 to Ethernet Adapter](https://www.amazon.co.uk/Anker-AK-A7611011-USB-1000Mbit-networking/dp/B00PC0P2DI?ie=UTF8&*Version*=1&*entries*=0)

* [ANKER USB 3.0 to RJ45 Gigabit Ethernet Adapter](https://www.amazon.co.uk/dp/B00NPJP33M/ref=pd_lpo_sbs_dp_ss_1?pf_rd_p=569136327&pf_rd_s=lpo-top-stripe&pf_rd_t=201&pf_rd_i=B00DNU8Y20&pf_rd_m=A3P5ROKL5A1OLE&pf_rd_r=C5N2DD7H2D7AVRXM1VHP)

I have not tested it, but other devices based on the same chipset should work, such as the [TP-LINK UE300](https://www.amazon.co.uk/gp/product/B00YOKMKE6/ref=pe_1959711_130662621_em_1p_0_ti)


## Performance

I have been testing the drivers for almost two months now and performance has been rock solid, and on a par with the onboard Intel adapter or the Realtek Mini PCIe adapter I use on the [NUC Squarepants](/NUC-Squarepants). I had a few hiccups to start with, and that is detailed under the [ESXi quirks](#esxi-quirks) section below. 

### iPerf figures for the ASIX driver

![ASIX 88179_178a](/images/usb/iperf_asix.png){: .align-center}

### iPerf figures for the Realtek driver

![RTL8153](/images/usb/iperf_rtl.png){: .align-center}

Using iPerf alone is not a reliable way of measuring throughput, but it gives a good indication. I have, however, performed many vMotion operations to get better "real world" figures. For example, migrating a VM assigned 8 GB of RAM (VCSA), host only, takes ~4 seconds; migration to another host and datastore (iSCSI to internal disk) around ~4 minutes. Those figures are pretty much identical to what I see when the same operations are performed using the onboard Intel adapter. 

## Device details

![lsnics](/images/usb/lsnics.png){: .align-center}

As can be seen above both devices show up as "Pseudo" devices, but have very different names. The reason for that is that the Realtek driver is CDC-Ether compliant, whereas the ASIX driver is not. One approach is no better than the other, though. 

**ASIX**

![getnic](/images/usb/asix_getnic.png){: .align-center}

![getnic](/images/usb/asix_ethtool.png)

**Realtek**

![getnic](/images/usb/rtl_getnic.png){: .align-center}

![getnic](/images/usb/rtl_ethtool.png)


## ESXi quirks


### Stacks

As you can imagine I was very happy that I managed to get the ASIX driver working, but I noticed from the beginning that whilst egress (TX) throughput was in line with gigabit speed, ingress (RX) was at least 300 Mbits/sec less. I exchanged a few emails with William Lam, and he was also seeing the same lower throughput (sometimes even less). I tried tweeking the code every which way to no avail, and I came to the conclusion that this was the better we could get off of those adapters. I was miffed.

I started looking around the web and came across the ANKER adapter, noticing that it used a different chipset and driver. Emboldened by my success with the ASIX driver I turned my hand to the newly discovered Realtek driver. A few days later I had the driver compiled and working on ESXi 6.0, 5.5 and 5.1. Woo-hoo! 

Another round of iPerf tests revealed the exact same lower RX throughput with the new adapter (what?). Next, I moved the adapters around: the builtin NIC (vmnic0) was moved to vSwitch1 (iSCSI) and the USB adapter moved to vSwitch0. I had baseline test results for the Intel adapter, so I knew the throughput was the same for TX and RX. When I performed the same iPerf test again, this time with the Intel NIC on the other vSwitch, the RX throughput was lower too, as seen with the USB adapters... 

What could be causing this? The only thing I could think of was the fact that on vSwitch1 the ethernet traffic was tagged. Shirley that couldn't be the reason? And it wasn't -- it was routing. I have a Cisco SG300 running on Layer 3 mode (router) and it will happily do inter-VLAN routing, no problem. The difference on ESXi is that with the single TCP/IP stack design there is only the default gateway, and a different gateway cannot be assigned to interfaces on different VLANs (unlike most other sensible operating systems). Traffic was hitting the default gateway (VLAN 100), then being re-routed to the ISCSI VLAN (10). That worked fine on egress, but the return trip, bouncing from VLAN to VLAN, was killing the speed.

I dully created a custom TCP/IP stack for VLAN 10, which enabled me to then assign another gateway, as well as appropriate static routes. That immediately resolved the issue; but then I could not bind the vNIC anymore to the iSCSI adapter. Is the Custom TCP/IP Stack feature on ESXi actually working? Answers on a post card, please.

### The neighbourhood

I had kind of resolved the first issue, so I went on to test the speed of the USB adapter again. Remember that it was now on vSwitch0, home of the default gateway, so I was expecting everything to be fine. Egress, as always, fine; then I tried the other way around and... Boom! The speed was down on the floor, just unusable (double "what?").

It was so bad that I could not even keep the SSH sessions open anymore. Pinging the server resulted in multiple packets dropped, with the occasional response coming trough. Time to bring around the bloodhound (Wireshark) to see what was going on. I could not see packets hiting the interface at all -- they were actually hitting the other interface on the server (treble "What?")

Time to look at the ARP table from another server:

```sh
esxcli network ip neighbor list
Neighbor        Mac Address        Vmknic    Expiry  State  Type
--------------  -----------------  ------  --------  -----  -------
192.168.10.132  0c:c4:7a:a9:55:89  vmk1     873 sec         Unknown
--> 192.168.10.226   3c:97:0e:5e:a1:bd  vmk1    1190 sec         Unknown <--
192.168.10.232  d0:50:99:c0:ae:8f  vmk1     919 sec         Unknown
192.168.1.234   00:0c:29:97:66:3a  vmk0    1162 sec         Unknown
--> 192.168.1.226   3c:97:0e:5e:a1:bd  vmk0    1181 sec         Unknown <--
192.168.1.223   00:0c:29:13:d3:03  vmk0    1143 sec         Unknown
192.168.1.254   7c:69:f6:9a:c9:d0  vmk0     649 sec         Unknown
192.168.1.222   c0:3f:d5:64:ae:5d  vmk0    1130 sec         Unknown
192.168.1.240   14:b1:c8:00:37:80  vmk0    1173 sec         Unknown
```      
You can clearly see two different IP addresses linked to the same MAC address. Well, I thought, let's try clearing the ARP cache. 

On the other ESXi servers:

```sh
esxcli network ip neighbor remove --version=4 --neighbor-addr=192.168.1.226
esxcli network ip neighbor remove --version=4 --neighbor-addr=192.168.1.220
```
And on my own machine:

```sh
sudo arp -a -d
```
Ping the server again with ```arping```

```sh
arping -S 192.168.1.240 -i en8 192.168.1.226
ARPING 192.168.1.226
60 bytes from 00:50:56:67:91:a9 (192.168.1.226): index=0 time=318.050 usec
60 bytes from 00:50:56:67:91:a9 (192.168.1.226): index=0 time=318.050 usec
60 bytes from 00:50:56:67:91:a9 (192.168.1.226): index=1 time=276.089 usec
```
That is more like it!

{: .notice--info}
During development of the driver, I had loaded and unloaded the module whilst tailing the vmkernel.log so many times that I had memorised the MAC address. I knew that was the correct one.

Then I try to SSH to the server again, and nothing. Look at the ARP table, and the IP address is yet again listed against the wrong MAC address. What is going on here?

It was time for some search-fu to be applied. Hit the webs, and got this: [vmk0 management network MAC address is not updated when NIC card is replaced or vmkernel has duplicate MAC address (1031111)](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=1031111), which included this gem:

*The MAC address of vmk0 management network may not get updated after you replace or assign a new MAC address to the NIC and run the esxcfg-vmknic –l command from the command line. The default setting for the ESXi host is not to select the new hardware MAC address.*

The proposed solution? Delete and recreate the ```vmknic```. Not what I wanted to read, as I was going to be swapping the adapters around many times to complete my tests. But wait, there is a workaround:

<div class="notice--warning">
<p><b>Workaround</b></p>
<p>To work around the issue, manually configure the MAC address on the ESXi host:</p>
<p style="margin-left: 40px">1. In the troubleshooting console, run the command:</p>
	<p style="margin-left:60px">esxcfg-advcfg -s 1 /Net/FollowHardwareMac</p>
<p style="margin-left: 40px"> 2. Restart the ESXi server.</p>
</div>

After applying the workaround I was then able to move the physical adapters freely between ```vmknics``` and the MAC address changed as expected. 

I understand that moving physical adapters around is not something that would be done regularly, but I would have preferred if the "workaround" was actually the default behaviour. Having said that, I changed stuff around, changed ESXi versions, and moved adapters so many times on that server that I am surprised I did't hit any other problems...  

## Compiling the drivers

I will not elaborate on how to compile the drivers here. If you are interested, I have some reasonably detailed steps and also build scripts accompanying the source code on GitHub:

* Repository for the [ASIX ax88179_178a](https://github.com/gomesjj/ax88179_178a) driver.
* Repository for the [Realtek r8152](https://github.com/gomesjj/r8152) driver.


## TL;DR - Just gimme the driver

OK, OK. You are impatient...

You can download the VIBs using the following links:

### ASIX


#### ax88179-1.14.0-1-esxi60u2.vib 
[ ![Download](https://api.bintray.com/packages/gomesjj/VIBs/ax88179-1.14.0-1-esxi60u2.vib/images/download.svg) ](https://bintray.com/gomesjj/VIBs/ax88179-1.14.0-1-esxi60u2.vib/_latestVersion)


#### ax88179-1.14.0-1-esxi55u3.vib

 [ ![Download](https://api.bintray.com/packages/gomesjj/VIBs/ax88179-1.14.0-1-esxi55u3.vib/images/download.svg) ](https://bintray.com/gomesjj/VIBs/ax88179-1.14.0-1-esxi55u3.vib/_latestVersion)


#### ax88179-1.14.0-1-esxi51u3.vib

 [ ![Download](https://api.bintray.com/packages/gomesjj/VIBs/ax88179-1.14.0-1-esxi51u3.vib/images/download.svg) ](https://bintray.com/gomesjj/VIBs/ax88179-1.14.0-1-esxi51u3.vib/_latestVersion)

### Realtek

#### r8152-2.06.0-1.esxi60u2.vib

[ ![Download](https://api.bintray.com/packages/gomesjj/VIBs/r8152-2.06.0-1.esxi60u2.vib/images/download.svg) ](https://bintray.com/gomesjj/VIBs/r8152-2.06.0-1.esxi60u2.vib/_latestVersion)


#### r8152-2.06.0-1.esxi55u3.vib

 [ ![Download](https://api.bintray.com/packages/gomesjj/VIBs/r8152-2.06.0-1.esxi55u3.vib/images/download.svg) ](https://bintray.com/gomesjj/VIBs/r8152-2.06.0-1.esxi55u3.vib/_latestVersion)


#### r8152-2.06.0-1.esxi51u3.vib

[ ![Download](https://api.bintray.com/packages/gomesjj/VIBs/r8152-2.06.0-1.esxi51u3.vib/images/download.svg) ](https://bintray.com/gomesjj/VIBs/r8152-2.06.0-1.esxi51u3.vib/_latestVersion)
