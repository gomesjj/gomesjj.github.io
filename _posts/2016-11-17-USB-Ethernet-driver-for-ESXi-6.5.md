---
title: USB 2.5G Ethernet drive support for ESXi 6.5 and 6.7
excerpt: "ESXi 6.5/.67 drivers for USB 3.0 Gigabit Ethernet 2.5G adapters based on the Realtek RLT8156 chipsets"
header:
  teaser: "/images/usb_adapters_65.png"
category: [Homelab]
tags: [Homelab, ESXi, USB, Ethernet]
---

<div class="notice--danger" markdown="1">
<b>Note</b></p> 
Do not update your existing VIB! The VIB should be removed, followed by a reboot and re-install. Updating the VIB will result on an inability to load the usbnet module.
<p></p>
</div> 

I know the future for ESXi is based on a Linux free World; but for those of us still rocking a Home Lab based on either ESXi 6.5 or 6.7, having the ability to step-up to the dizzying heights of better than Gigabit Ethernet, and for that matter, with USB based adapters, is quite something. Not to mention the fact that some of those adapters are quite inexpensive!

Some days ago I was contacted by someone based in the Netherlands who was trying to get the RTL8156 based adapters he had recently purchased working on ESXi. You might or might not have read this [piece](/homelab/Want-a-USB-Ethernet-driver-for-ESXi-You-can-have-two/) about USB Ethernet drivers for ESXi. I have been using both Realtek and ASIX adapters to complement the single Ethernet adapter on the Intel NUCs, and they have proved to be rock solid. 

Fast forward a few months, and as soon as ESXi 6.5 was announced people started asking if I could recompile the drivers for the new release. Finally I had some time this week to look into that. The result? A lot of wasted time downloading the 6.5 disclosure packages, setting up the environment, tweaking build scripts, etc. It turns out that compiling the drivers in the ESXi 6.0 environment I built previously worked much better, with just a single trivial change to the USB namespace.

The single change I had to make was to change the namespace dependencies map from this:

```sh
echo -e "VMK_NAMESPACE_REQUIRED(\"com.vmware.usb\", \"9.2.3.0\");\
\nVMK_NAMESPACE_REQUIRED(\"com.vmware.usbnet\", \"9.2.3.0\");"\
```

To this:

```sh
echo -e "VMK_NAMESPACE_REQUIRED(\"com.vmware.usb\", \"10.0\");\
\nVMK_NAMESPACE_REQUIRED(\"com.vmware.usbnet\", \"9.2.3.0\");"\
```

Note the sneak change introduced by VMware -- the USB namespace is version 10.0 now...

<div class="notice--warning" markdown="1">
**Update (07/02/19)**  

<p></p>

<li>Driver update to version 1.19.0 (Latest source code from ASIX).</li>   

<p></p>

**Update (25/02/19)**   

<p></p>
<li>Realtek driver updated to version 2.11.0 (latest)</li>
<li>Version 2.11.0 adds support for the upcoming 2.5G USB C Ethernet adapters (RTL8156; not tested)</li>
<p></p>

</div> 

{% include toc %}

## What's new

Quite a lot! Apart from the new functionality discussed in detail by the VMware Gurus elsewhere, looking at the latest ODP packages clearly reveals VMware's intention to move away from what they call "legacy" drivers.

The USB Ethernet drivers are dependent on two legacy modules (usb and usbnet); the modules are still available in ESXi 6.5, but will not load by default. 

My first attempt at loading the USB Ethernet drivers failed miserably. It took me some time to realise that in 6.5 all legacy USB drivers (xhci, ehci-hcd, usb-uhci, usb, usb-storage, etc.) have been replaced by a single native driver called vmkusb. It serves me right for not paying attention to the various announcements...

Anyway, in order to get the USB Ethernet drivers to load the vmkusb module must be disabled for the legacy USB drivers to load. The details are described in the VMware Knowledge Base article [2147650](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=2147650).

Other than the above, there are no material differences between 6.0 and 6.5 for the legacy adapters so all performance figures described on the previous article are still valid.

## Tested devices

The following devices were tested with these drivers.

### ASIX

* [StarTech USB 3.0 to RJ45 Ethernet LAN 10/100/100 Network Adapter](https://www.amazon.co.uk/gp/product/B0095EFXMC/ref=oh_aui_detailpage_o04_s00?ie=UTF8&psc=1)

* [StarTech USB 3.0 to Dual Port Gigabit Ethernet Adapter NIC with USB Port](https://www.amazon.co.uk/gp/product/B00D8XTOD0/ref=oh_aui_detailpage_o03_s00?ie=UTF8&psc=1)

* [Plugable USB 3.0 to 10/100/1000 Gigabit Ethernet LAN Network Adapter](https://www.amazon.co.uk/gp/product/B00AQM8586/ref=oh_aui_detailpage_o02_s00?ie=UTF8&psc=1)


### Realtek

* [ANKER Aluminum USB 3.0 to Ethernet Adapter](https://www.amazon.co.uk/Anker-AK-A7611011-USB-1000Mbit-networking/dp/B00PC0P2DI?ie=UTF8&*Version*=1&*entries*=0)

* [ANKER USB 3.0 to RJ45 Gigabit Ethernet Adapter](https://www.amazon.co.uk/dp/B00NPJP33M/ref=pd_lpo_sbs_dp_ss_1?pf_rd_p=569136327&pf_rd_s=lpo-top-stripe&pf_rd_t=201&pf_rd_i=B00DNU8Y20&pf_rd_m=A3P5ROKL5A1OLE&pf_rd_r=C5N2DD7H2D7AVRXM1VHP)

* [TP-LINK UE300 USB 3.0 to Gigabit Ethernet Network Adapter](https://www.amazon.co.uk/gp/product/B00YOKMKE6/ref=pe_1959711_130662621_em_1p_0_ti)

* [Rankie SuperSpeed USB 3.0 to RJ45 Gigabit Ethernet Network Adapter](https://www.amazon.co.uk/gp/product/B010SEARPU/ref=ox_sc_act_title_1?ie=UTF8&psc=1&smid=A7ZMMLW05YAY7)

Tested by Glen Kemp

* [Anker Unibody 3-Port USB 3.0 and Ethernet Hub](https://www.amazon.co.uk/Anker®-Unibody-Ethernet-RTL8153-Chipset/dp/B00PC0J1VC/ref=sr_1_1?s=computers&ie=UTF8&qid=1464184877&sr=1-1&keywords=Anker+Unibody+3-Port+USB+3.0+and+Ethernet+Hub)

USB 2.0 Adapter (RTL8152B Chipset)

* [TP-LINK UE200 USB 2.0 to 100 Mbps Ethernet Network Adapter](https://www.amazon.co.uk/TP-LINK-UE200-Ethernet-Foldable-Ultrabook/dp/B01GRY7RHG)  

Tested by Glen Kemp  

* [Smays 3-Port OTG USB-HUB and USB2.0 RJ45 Ethernet Network Adapter](https://www.amazon.co.uk/gp/product/B00WR6A57S/ref=as_li_ss_tl?ie=UTF8&psc=1&linkCode=sl1&tag=s0517-21&linkId=5815c60c53524b534b98dcd596eab09c)


## The drivers

You can download the VIBs using the following links:

### ASIX

#### ESXi 6.5/6.7 VIB 

[Download](https://devtty.jfrog.io/ui/native/default-generic-local/Asix/ax88179-1.15.1-1_esxi65.vib)

### Realtek

#### ESXi 6.5/6.7 VIB

[Download](https://devtty.jfrog.io/ui/native/default-generic-local/Realtek/r8152-2.12.0_vmw.650.x86_64.vib)
