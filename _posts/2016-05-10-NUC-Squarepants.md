---
title: NUC Squarepants
excerpt: "Adding a Mini PCIe Ethernet adapter to 3rd or 4th generation Intel NUC, housed on a 3D printed custom base."
header:
  teaser: "/nuc/nuc_squarepants.png"
category: [Homelab] 
tags: [Homelab, Virtualisation, NUC]
---

My first Intel NUC was yet to be delivered, but I was already looking around for a solution for it's greatest shortcoming: the single Ethernet adapter. So, here is how my first attempt at solving that went. 

As I mentioned in my previous post about the evolution of my [home lab](/homelab/Intel-NUC-to-the-rescue), I decided to test the waters with an Intel NUC [DC53427HYEA](http://www.intel.co.uk/content/www/uk/en/nuc/nuc-kit-dc53427hye-board-d53427rke.html). I was as yet unsure as to whether or not the NUC would be an ESXi host, but I knew I could run Windows Server 2012 on it. If I couldn't get a second NIC for ESXi, the NUC would still have a purpose as my new Domain Controller. 

{: .notice--info}
As an aside, I chose this older NUC model, and later the [NUC5i5RYH](http://www.intel.co.uk/content/www/uk/en/nuc/nuc-kit-nuc5i5ryh.html), because they are the only models in the line up to include Intel AMT. I think running with slightly older models is a price worth paying in exchange for remote out-of-band management.

*[AMT]: Active Management Technology

Well, back to our quest... I am averse to reinventing the wheel, so I started by searching for existing solutions, and found surprisingly few: this [Adding a second NIC to a 5th Gen Intel NUC](http://www.virten.net/2015/09/adding-a-second-nic-to-a-5th-gen-intel-nuc-or-other-pcie-cards/) by Florian Grehl, and this [Adding a Second Ethernet Port to an Intel NUC via Mini PCIe](http://blog.fosketts.net/2015/06/05/adding-a-second-ethernet-port-to-an-intel-nuc-via-mini-pcie/) by Stephen Foskett. Both solutions are very imaginative, but not quite what I had in mind.

I didn't like the idea of running a full length PCIe Ethernet adapter outside the NUC enclosure like Florian did. Plus, there is a need for a second 12V power adapter to drive the NIC. Ah, and I didn't have a 5<sup>th</sup> generation NUC as yet...

Stephen's solution was closer to what I had in mind, but not quite. Using a Mini PCIe Ethernet adapter housed inside a custom base sounded just right for my NUC model, but I din't fancy soldering the adapter directly to the board! However, I did like the idea of a custom 3D printed base for the NUC; I thought perhaps I could combine the best aspects of each approach: a Mini PCIe Ethernet adapter connected by some sort of extender, and housed in a custom base. Sounded simple enough!
 
Stephen had posted a link to his [3D model](https://www.tinkercad.com/things/6cVLKjO38uJ-intel-nuc-disk-and-ethernet-base), so that is what I started with. Unfortunately, the design was only available as an STL file, which could not be modified to match my own NUC model. His custom base was also meant to house a 2.5" drive, something I didn't want or need. Luckily, a chap called David Johnston had already remixed Stephen's design and published it in Parametric OpenSCAD format on [Thingverse](http://www.thingiverse.com/thing:999900), ready to be modified. I just had to learn a bit about OpenSCAD.

Without further ado, I present to you the NUC Squarepants design:

![NUC Squarepants](/images/nuc/nuc_squarepants.png){: .align-center} 
   
OK, it doesn't look quite like that. We will see how it really looks like in a while, but first, here is the shopping list.

### Components

* Intel NUC 3<sup>rd</sup> or 4<sup>th</sup> generation (with mPCIe/mSATA)
* [Syba Mini PCI-E Gigabit Ethernet Card](https://www.amazon.co.uk/dp/B00B524102/ref=cm_cr_ryp_prd_ttl_sol_0) **or**
* [Startech Mini PCI Express Gigabit Ethernet Network Adapter](https://www.amazon.co.uk/dp/B006VCPB2S/ref=cm_cr_ryp_prd_ttl_sol_5)
* [Mini PCI Express Extender](https://www.amazon.co.uk/dp/B00T2FP7X4/ref=cm_cr_ryp_prd_ttl_sol_3)
* [Modified SCAD file for the 3D base](https://github.com/gomesjj/nuc-smartpants/blob/master/nuc_box_ver3.scad)

The StarTech adapter costs twice as much as the Syba. I bought both and would say the Syba is a better bet, as the performance is identical (both are based on the Realtek R8111 chipset).

This is what the Syba and StarTech adapters look like:

![Syba mPCIe Adapter](/images/nuc/syba.png) ![Syba mPCIe Adapter](/images/nuc/startech.png)

And this is the mPCIe extender:

![Syba mPCIe Adapter](/images/nuc/mpcie_extender.png){: .align-center}

{: .notice--info}
**Note:** The small board on the left is connected to the mPCIe interface in the motherboard.

### Putting it all together

1\. Remove the bracket from the Ethernet adapter, disconnect the cables and fix the RJ45 daughterboard to the custom base.

![Syba mPCIe Adapter](/images/nuc/2_nuc_base_phy.png){: .align-center}

2\. Connect the extender to the lower slot on the motherboard (the top one is mSATA). There are perforated lines in the PCB marking where to snap it according to the required length.

![Syba mPCIe Adapter](/images/nuc/1_nuc_board_adapter.png){: .align-center}
	
3\. Fix the second half of the extender (with the mPCIe connector) to the custom base.

![Syba mPCIe Adapter](/images/nuc/3_nuc_base_adap.png){: .align-center}   
 
4\. Plug the main board of the Ethernet adapter to the extender in the custom base:

![Syba mPCIe Adapter](/images/nuc/4_nuc_base_eth.png){: .align-center} 

5\. The custom base should look like this once all the cables are connected:

![Syba mPCIe Adapter](/images/nuc/5_nuc_base_complete.png){: .align-center}

6\. Connect the flat ribbon between the base and the main board:

![Syba mPCIe Adapter](/images/nuc/6_nuc_base_board.png){: .align-center}

**Note:** The flat ribbon is tucked away slightly to clear the stand-off for the mSATA adapter

![Syba mPCIe Adapter](/images/nuc/6a_ribbon_detail.png){: .align-center}

7\. Carefully loop the flat ribbon and attach the custom base to the NUC. The base was designed with long screw posts to accommodate the original screws. Et voilà, the real NUC Squarepants:

![Syba mPCIe Adapter](/images/nuc/7_nuc_complete.png){: .align-center}

So we now have a NUC with a new pair of pants large enough to accommodate it's extra  package. Oo-er missus!

{: .notice--warning}
**I know, I know. That is not a pair of pants, the base is not really square and there is no tie... but I like the name NUC Squarepants. I must be going senile.**

### Making it all work

There is no out-of-the-box support for Realtek adapters on ESXi, so a driver will need to be installed. I will just point you in the direction of the excellent [VIBSDepot](https://vibsdepot.v-front.de/wiki/index.php/List_of_currently_available_ESXi_packages) -- just grab the ```net55-r8168``` VIB and you should be sorted.

{: .notice--info}
**Note:** If you are not running ESXi 6.0 or 5.5 Update 3, you will also need a driver for the on-board Intel NIC. You need the ```net-e1000e``` VIB, so get it too whilst you are at it.

### Ether device details

![Physical adapters](/images/nuc/mpcie_rtl_8111.png)

![getnics](/images/nuc/getnics.png)

Interestingly, only *rx-checksuming* is enable for this driver; there is no way to set *tx-checksuming*, *sc* and *tso*, but the driver throughput is on a par with the Intel onboard NIC.

![ethtool](/images/nuc/ethtool.png)

### Later generation NUCs

This solution does not work for the 5<sup>th</sup> and later generation NUCs, as the mPCIe slot has been replaced by an M.2 slot. If you don't mind running with a NIC outside the NUC case and a second power adapter, then Florian's [solution](http://blog.fosketts.net/2015/06/05/adding-a-second-ethernet-port-to-an-intel-nuc-via-mini-pcie/) is an option. Otherwise, come along this [way](/homelab/Want-a-USB-Ethernet-driver-for-ESXi-You-can-have-two/) for a solution that will work on all generations of the NUC (or anything else with a USB port).
