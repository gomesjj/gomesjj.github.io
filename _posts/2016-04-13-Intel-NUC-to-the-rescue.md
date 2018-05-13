---
title: Intel NUC to the rescue
excerpt: "Updating my home lab with Intel NUCs and a self-build NAS based on the Supermicro A1SAi-2750F board"
header:
  teaser: "/images/intel-nucs.png"
category: [Homelab] 
tags: [Homelab, Virtualisation, Avoton, NUC]
---

The components of my home lab changed many times over the years, but lately I embarked on a different approach: I wanted to come up with a design that kept the power consumption to a minimum. Spending thousands of £ per year on the electricity bill started to upset the GLW. The green credentials of my lab were also generally lacking.

*[GLW]: Good Lady Wife

I talked about my current set-up in this [post](/homelab/The-Home-Lab/). Some of my servers are quite old now (still serviceable, though), so it is understandable that the power requirements are high. The IBM POWER5 p505 server, in particular, slurps electricity as if there was no tomorrow.

So, I deployed my search-fu skills and came to the conclusion that I had two options: build something based on the Intel Avoton (Atom C2000 series) or go with the Intel NUC. I also looked briefly at the Mac Mini, but the latest models with soldered on memory didn't appeal to me. In the end, I plumped for both an Avoton self-build based around the [Supermicro A1SAi-2750F](https://www.supermicro.com/products/motherboard/ATOM/X10/A1SAi-2750F.cfm) and an Intel NUC [DC53427HYEA](http://www.intel.co.uk/content/www/uk/en/nuc/nuc-kit-dc53427hye-board-d53427rke.html) to try them out. 

The Atom C2750 eight-core is a small beast: enough grunt to play the ESXi game, but with a wallet friend 20W TDP. On the other hand, the NUC I chose, albeit third generation, was also pretty decent (17W TDP). The downside? Maximum 16GB of RAM and a single Ethernet adapter. 

*[TDP]: Thermal Design Power

In the end, I decided to buy three more NUCs (another DC53427HYEA and two [NUC5i5RYH](http://www.intel.co.uk/content/www/uk/en/nuc/nuc-kit-nuc5i5ryh.html)) to power my minuscule VMware cluster. One of the reasons was aesthetics: I just wanted the smallest possible footprint for the lab; and the other was the challenge of coming up with a way to add a second NIC to the little beauties. 😎 

"What about the Atom Board?" you might ask. Well, I decided to build a FreeNAS server with that. I will be elaborating on my NAS set-up in another post sometime. Meanwhile, you can see how I resolved the issue of the single Ethernet adapter in the NUC in this [post](/homelab/NUC-Squarepants/) and [this](/homelab/Want-a-USB-Ethernet-driver-for-ESXi-You-can-have-two/).
