---
title: NUC Squarepants
header:
  teaser: "nuc_squarepants.png"
category: [HomeLab] 
tags: [HomeLab, Virtualisation, NUC]
---

My first Intel NUC was yet to be delivered, and I was already looking around for a solution for it's greatest shortcoming: the single Ethernet adapter. So, here is how my first attempt at solving that went. 

As I mentioned in my previous post about the evolution of my [home lab](/Intel-NUC-to-the-rescue), I decided to test the waters with an Intel NUC [DC53427HYEA](http://www.intel.co.uk/content/www/uk/en/nuc/nuc-kit-dc53427hye-board-d53427rke.html). I was as yet unsure as to whether or not the NUC would be an ESXi host, but I knew I could run Windows Server 2012 on it as a new Domain Controller. If I couldn't get a second NIC for ESXi, the NUC would still have a purpose. 

As an aside, I chose this older NUC model, and later the [NUC5i5RYH](http://www.intel.co.uk/content/www/uk/en/nuc/nuc-kit-nuc5i5ryh.html), because they are the only models in the line up to include Intel AMT.

*[AMT]: Active Management Technology
