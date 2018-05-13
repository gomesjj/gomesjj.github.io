---
title: The Home Lab
header:
   teaser: "/images/dc.png"
category: [Homelab] 
tags: [Homelab, Education, Virtualisation, NAS]
---

Like most technical people I have a home lab. Actually, I've had one for many years now and the lab became even more important once I moved from engineering roles to become a paper pusher (Architect). You see, I really like keeping up with the latest technologies, and more importantly, keep the skills up-to-date. 

When we first moved into this house (10 years ago) I took the opportunity to lift the floor boards -- suspended floors here in the UK -- and run CAT5 and Coaxial all over. The cable runs terminated at the first floor, inside an airing cupboard (That is where the BT master socket was. Don't ask!). Due to the limited space, I installed a [Minitran 10" inch 6U rack](http://www.minitran.co.uk/pages/products/list.mhtml?ct=31&sc=107) complete with 2 x patch panels, 1 x Voice Panel, 2 x Power Distribution units and 1 x Compact Ethernet Switch. The switch was the first one to go soon after, as it was only a 10/100 job.

The servers were all racked up in the loft, which worked great in winter, but not too well in summer (yes, we do have summers in England). So I got myself a Cisco SG300-10 linked via OM2 fibre to a Cisco SG200-18 in the garage and moved all the servers there. In the process, I bought an 
Aiino ClusterMaster 12U rack to house the servers. This rack is superb -- originally designed for the Apple Xserve and Xserve RAID it includes 4 large fans in the back, a 9 x connector power strip and plenty of sound proofing to keep things quiet:

![Aiino ClusterMster](/images/aiino-clustermaster.png){: .align-center}

The Aiino rack houses the following kit:

* Cisco SG200-18
* NEC Express5800/R120a-1 (ESXi server)	
	* 2 x Intel Xeon E5504 @ 2GHz
	* 32GB RAM
	* 3 x SAS/SATA 3.5" drives
* NEC Express5800/R120a-2 (Windows Server 2012 Hyper-V host)
	* 1 x Intel Xeon E5504 @ 2GHz
	* 20GB RAM
	* 6 x SAS/SATA 2.5" drives
* Sun Fire X4240 (Solaris 11.2 NAS)
	* 2 x Quad-Core AMD Opteron Processor 2380 @ 2.5GHz
	* 40GB RAM
	* 16 x SAS/SATA 2.5" drives
* Dell R210 PowerEdge server (Windows 2012 Domain Controller)
	* Dual Core Xeon @1.2GHZ
	* 10GB RAM
	* 2 x SATA 3.5" drives
* IBM pSeries POWE5 9115-505 (PowerVM host)
	* 1-core @ 1.9GHz
	* 16GB RAM
	* 2 x DASD 3.5" drives
	* HMC 7.7.4 running as a VM

Connection to the  Internet (BT Infinity FTTC) is handled by a Cisco 887VA router. Great piece of kit providing both IPSEC and SSL VPN, as well as better throughput than the standard BT modem. Wi-Fi is taken care of by an Apple Airport Extreme base station and a handful of Apple Airport Express bases around the house. 

## Meet the Chief Architect

No changes to the Home Lab will happen without approval from the Chief Architect!

![Chief Architect](/images/chief_architect.png){: .align-center}
