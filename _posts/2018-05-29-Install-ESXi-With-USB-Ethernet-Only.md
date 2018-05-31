---
title: Install ESXi on a server/laptop with only USB Ethernet
excerpt: "VMware Weasel hack to allow installation of ESXi on server/laptop with only a USB Ethernet adapter."
header:
  teaser: "/images/no_adapter.png"
category: [Homelab]
tags: [Homelab, ESXi, USB, Ethernet]
---

It has been more than a year since I wrote about the ASIX and Realtek USB Ethernet drivers ( [here](/homelab/Want-a-USB-Ethernet-driver-for-ESXi-You-can-have-two/) and [here](/homelab/USB-Ethernet-driver-for-ESXi-6.5/) ), and I am still getting quite a lot of interest, success reports, bug reports and requests for help. One of the commonest requests has been a way to install ESXi when the target machine doesn't have a built-in Ethernet adapter.

Now, one would expect to be able to whip a customised ISO installer with the USB Ethernet drivers, boot from it and be able to install ESXi. Sadly, that is not the case.

I tried to come up with various "solutions", including a custom kickstart file to either set the network or the netdevice, but nothing worked. That was a few months ago, but I have recently managed to find some time to dedicate to the issue... Guess what? Network configuration is hard-coded to use vmnic0.

<div class="notice--warning" markdown="1">  

**Update (19/05/16)**  

I have changed the solution to use the first physical NIC device which is reporting link up state. No hardcoding -- yeah!

<p></p>

</div>

## Weasel

Weasel is VMware's operating system installer, which is very similar to RedHat's Anaconda. Weasel was originally a "Fling" that was released in 2010 as an Open Source [project](https://github.com/vmware/weasel).

So, I started by perusing the GitHub repository (mainly Python scripts), but I couldn't identify anything odd. Hmmm! So, I jumped on one of my existing ESXi servers and started the search again. Lo and behold, the actual packages in the server have almost no resemblance to the GitHub source code... Weaselly indeed!

## The hack

Once I identified the script that had the adapter hardcoded (applychoices.py) it didn't take very long to work out a hack to overcome that. It is not pretty, and involves more hard-coding, but it works.

Here is the how to:

## Editing and repackaging the VIB

Copy the VIB (weaselin.t00), say, to /tmp and extract the contents to a suitable sub-directory:

``` cp /bootbank/weaselin.t00 /tmp/ ```  
``` cd /tmp ```  
``` vmtar -x weaselin.t00 -o weaselin.tar ```  
``` mkdir weaselin_mod ```   
``` cd weaselin_mod ```  
``` tar -xf ../weaselin.tar ```    

Edit networking/networking_base.py:  

vi -c 70 networking/networking_base.py   

Add the following functions:  

```  

# ----------------------------------------------------------------------------
def getFirstPluggedInPhysicalNic():
    ''' Return the first pnic object which is reporting linkUp state'''
    for pnic in [pnicPtr.get() for pnicPtr in _netInfo.GetPnics()]:
        if pnic.IsLinkUp():
            return pnic[0]
    return None

# ----------------------------------------------------------------------------
def getPluggedInPhysicalNicName():
    ''' Return a device name string of the first pnic which is reporting linkUp state'''
    pnic = getPluggedInPhysicalNic()
    if pnic:
        return pnic.GetName()
    return None
    
```

Edit "applychoices.py":  
  
``` vi -c 154 usr/lib/vmware/weasel/applychoices.py ```  
  
Change line 154 from:  
   
~~``` device = networking.findPhysicalNicByName('vmnic0') ```~~  
   
~~To this for a Realtek adapter:~~    
   
~~``` device = networking.findPhysicalNicByName('vmnic32') ```~~ 
   
~~Or this for an ASIX adapter:~~ 
   
~~``` device = networking.findPhysicalNicByName('vusb0') ```~~   

To this:   

``` device = networking.getFirstPluggedInPhysicalNicName() ```  

Recreate the tar file:  
   
``` tar -cvf ../weaselin.tar * ```   
``` cd ../ ```   

Repackage the VIB:  

``` vmtar -c weaselin.tar -o weaselin.vtar ```  
``` gzip < weaselin.vtar > weaselin.t00 ```   

Copy the customised Weasel VIB to a computer where you can generate a customised ESXi installer. Since ESXi 6.5 there has been a new native USB driver (vmkusb) that replaces what VMware call legacy USB drivers (XHCI/EHC/UHCI/OHCI). The new driver needs to be disable in order for the USB Ethernet adapters to work. The easiest way to achieve that is to remove the vmkusb driver from your custom ISO.

### Customised ISO image

The next step is to create a custom ESXi ISO installer, incorporating the relevant USB Ethernet driver. 

I normally use the excellent [v-Front.de Customizer.ps](https://www.v-front.de/p/esxi-customizer-ps.html) to do that. Make sure to use the "--pkgDir" option to add the USB VIBs and the "--remove" option to get rid of the new "vmkusb" driver.

Once the ISO is created, you can use a tool such as [UNetbootin](https://unetbootin.github.io) to write the ISO to a bootable USB stick. Simply overwrite the weasilin.t00 VIB with the one created in the steps above. 

### Too much work! Give me the VIBs

~~You can also download the customised Weasel VIBs using the following links:~~

~~### ASIX~~

~~### Realtek~~


Download the VIB, then copy the weasilin.t00 VIB to your bootable USB stick.  

[ ![Download](https://api.bintray.com/packages/gomesjj/VIBs/weaselling.t00.zip/images/download.svg?version=1.1) ](https://bintray.com/gomesjj/VIBs/weaselling.t00.zip/1.1/link)  


