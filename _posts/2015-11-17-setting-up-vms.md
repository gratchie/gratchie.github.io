---
layout: post
title: "Setting up the VM's"
published: true
tags: virtualbox
---

I'm using VirtualBox since it's free, stable and works well with OSX. If I'm deploying my lab from a linux machine, I will most likely use KVM since it is included in the EX200/300 directives.

####VirtualBox Installation

* Install [VirtualBox](http://download.virtualbox.org/virtualbox/5.0.10/VirtualBox-5.0.10-104061-OSX.dmg)

* Install [VirtualBox Extension Pack](http://download.virtualbox.org/virtualbox/5.0.10/Oracle_VM_VirtualBox_Extension_Pack-5.0.10-104061.vbox-extpack)

* Create a "Host-Only Network". This command will create the default "vboxnet0" host-only network.   

    `VBoxManage hostonlyif create`

* Disable VirtualBox dhcp server

    `VBoxManage dhcpserver --disable`

Now we are ready to create the VMs.

####Creating the VM's

I use this script to create VM's from command line. This is for Centos 7.1 with 8GB disk and 512MB RAM. Networking is also configured with Host-Only nic.

```bash
#!/bin/bash
# Copyright (c) 2015 Grace Thompson Rights Reserved.
# Create virtualbox VM's automatically
# Version: Centos 7.1
# Update $ISO path as needed


printUsage() {
  echo "vboxnodes-cent7.sh (vmhostname)"
  echo "Ex: vboxnodes-cent7.sh linux0101"
}

ISO="/ISO/CentOS-7-x86_64-DVD-1503-01.iso"

[[ -n "$1" ]] || printUsage

echo "Setting up VM $NAME"

for NAME in $1 ; do
  cd ~
  VBoxManage createvm --name $NAME --register --ostype RedHat_64
  VBoxManage createhd --filename $NAME.vdi --size 8000
  VBoxManage modifyvm $NAME --memory 512 --acpi on --boot1 dvd --boot2 disk \
             --nic1 hostonly --hostonlyadapter1 "vboxnet0"
  VBoxManage storagectl $NAME --name "SATA Controller" --add sata --portcount 1
  VBoxManage storageattach $NAME --storagectl "SATA Controller" \
             --port 0 --device 0 --type hdd --medium $NAME.vdi
  VBoxManage storageattach $NAME --storagectl "SATA Controller" \
             --port 1 --device 0 --type dvddrive \
             --medium $ISO

echo ""
echo "VM $NAME has been successfully created"

done
```

Proceed with Centos install after creating the VMs. 













<img src="http://octodex.github.com/images/dojocat.jpg" width="200" height="200" />
