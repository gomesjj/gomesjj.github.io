---
title: The Mini Lab
excerpt: "The evolution of the home lab: Intel Avoton, Intel NUC, FreeNAS, ESXi and FreeNAS"
header:
   teaser: "mini_lab_small.png"
category: [Homelab] 
tags: [Homelab, Education, Virtualisation, NAS, NUC]
---  

{% include toc %}

## Burning the money (don't tell the wife)  
  
I wrote about my old set-up in this [post](/homelab/The-Home-Lab/) and then again about the future state of my Home Lab [here](/homelab/Intel-NUC-to-the-rescue/), when I mentioned my intention of doing something to placate the GLW. See, my electricity bill was going well past £4k a year...   

*[GLW]: Good Lady Wife

Anyway, at the time of writing the second article (April 2016) I had one [DC53427HYEA](http://ark.intel.com/products/74483/Intel-NUC-Kit-DC53427HYE) (my physical AD controller), so I decided to buy another two NUCs, but this time the [NUC5i5RYH](http://www.intel.co.uk/content/www/uk/en/nuc/nuc-kit-nuc5i5ryh.html). A few weeks later I bought yet another NUC5i5RYH, so I could play with vSAN too...

For the NAS, I had settled on building something around the [ASRock C2750D41](http://www.asrockrack.com/general/productdetail.asp?Model=C2750D4I#Specifications), but shortly after, I also bought a [Supermicro A1SAi-2750F](https://www.supermicro.com/products/motherboard/ATOM/X10/A1SAi-2750F.cfm).

You would have thought that that was enough by now, and any sane person would agree, but not me! The ASRock board was going to be the foundation for my FreeNAS build (what with 12 SATA ports and all), but, six of the SATA ports are controlled by Marvell chipsets and they simply suck. Instead, I used the Supermicro board for my NAS with a cheap Dell PERC H200 HBA flashed to IT mode, and finally crossflashed with the LSI 9211i8i firmware. But then I had an idea -- Hey, what about resilience for the data? -- so another A1SAi-2750F lightened my wallet further...  

## Let's get physical  

The network infrastructure remains the same: a Cisco SG200-18 with an etherchannel link via OM2 fibre link to an SG300-10 (on layer 3 mode). Access to the networks beyond (Internet) goes trough a Cisco rv320 router. It might change soon, but that is for another post...   

There are five VLANs routed by the SG300-10 switch:  

|VLAN ID  | Purpose    |   
--------- | -----------  
|1  		| DRN        |
|10       | Management |
|20       | vSAN       |
|30       | vMotion    |
|40       | Guest Wi-Fi| 

### DRN (Domestic Routed Network)   

That is where all the home gear (laptops, desktops, home wifi, etc.) sits.

* Cisco SG300-10
* DC Controller
	* Intel DC53427HYE
	* 8GB RAM

### Mini Lab (VLANs 10, 20 and 30)  

* Cisco SG200-18
* NAS	
	* Lian Li PC-Q25B case
	* Supermicro A1SAi-2750F
	* 32GB RAM
	* 6 x SATA 4TB drives
* vSAN Cluster (3 nodes)
	* Intel NUC5i5RYH
	* 32GB RAM
	* 1 x 128GB M.2 SATA drive
	* 1 x 250GB SATA SSD drive
	* 2 x USB 3.0 Ethernet adapters
* Nested ESXi Host
	* Streacom F7CWS ALPHA Black case
	* 64GB RAM
	* 2 x 250GB SATA SSD drives
	* 1 x 1TB SATA drive  

**Note:** The NUCs are now housed on my Lego NUC Rack. I will be writing another post with instructions on how to build a rack just like that soon (maybe!).

### DR Lab (Streched VLANs 10, 20 and 30)

* Cisco SG200-18  

Still being built. I am thinking about getting an SG-500 switch to replace the SG-300-10. The DR lab would then go to the bottom of the garden. ;-)

At the moment, just a second NAS with the same specification as that of the mini lab. Data replicated via ZFS send/receive. 

## The Chief Architect says:

![Chief Architect](/images/chief_architect.png){: .align-center}  

<center>A reasonable effort, but could do better.</center>
