---
title: PfSense-WAN-LAN-DMZ
date: 2024-01-24 14:30:45 +0100
categories: [Network, Firewall]
tags: [HomeLab, security]     # TAG names should always be lowercase
---

# Schema

![Schema Network](../assets/img/pfsense-wan-lan-dmz/schema.png)


# Install PfSense

## Create VM on proxmox

> Creation virtual machine


![Creation vm pfsense](../assets/img/pfsense-wan-lan-dmz/creation-vm-pfsense.png)

![Creation vm pfsense os](../assets/img/pfsense-wan-lan-dmz/creation-vm-pfsense-os.png)

![Creation vm pfsense system](../assets/img/pfsense-wan-lan-dmz/creation-vm-pfsense-system.png)

![Creation vm pfsense disks](../assets/img/pfsense-wan-lan-dmz/creation-vm-pfsense-disks.png)

![Creation vm pfsense cpu](../assets/img/pfsense-wan-lan-dmz/creation-vm-pfsense-cpu.png)

> vmbr0 is my wan interface, in other words, my network company
![Creation vm pfsense memory](../assets/img/pfsense-wan-lan-dmz/creation-vm-pfsense-memory.png)

![Creation vm pfsense network](../assets/img/pfsense-wan-lan-dmz/creation-vm-pfsense-network.png)

![Creation vm pfsense confirm](../assets/img/pfsense-wan-lan-dmz/creation-vm-pfsense-confirm.png)

## Attach another networks interfaces

>We need to attach another network interface on proxmox ( our S.O)

I create a network interface with ipv4 -> 11.11.11.11/24, thats the ip address that we access to pfsense.

![Network Attach Config](../assets/img/pfsense-wan-lan-dmz/network-attach-config.png)

![Network Attach List](../assets/img/pfsense-wan-lan-dmz/network-attach-list.png)

And add to pfsense machine:

![Network Attach List](../assets/img/pfsense-wan-lan-dmz/network-attach-machine-pfsense.png)


![Network Attach List](../assets/img/pfsense-wan-lan-dmz/network-attach-machine-pfsense-list.png)


## Pfsense installer

> Accept copyrigth

![pfsnse-installer-copyrigth](../assets/img/pfsense-wan-lan-dmz/pfsnse-installer-copyrigth.png)

> Set install pfSense
