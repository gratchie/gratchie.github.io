---
layout: post
title: "The Master Server"
published: true
---

I'm using VirtualBox since it's free, stable and works well with OSX. If I'm deploying my lab from a linux machine, I will most likely use KVM since it is included in the EX200/300 directives.

####VirtualBox Installation

Install VirtualBox

    http://download.virtualbox.org/virtualbox/5.0.10/VirtualBox-5.0.10-104061-OSX.dmg

Setup a Host-only Network on virtualbox

    VirtualBox -> Preferences -> Host-only Network -> Add a new Host-only Network

Create a new VM. This will be your master vm that will act as the dhcp/dns/tftp/proxy server to the rest of your vms.

```bash
#!/bin/bash
echo "hello friend"
```















<img src="http://octodex.github.com/images/dojocat.jpg" width="200" height="200" />
