---
title: PfSense WAN-LAN-DMZ
date: 2024-01-25 22:30:45 +0100
categories: [Network, Firewall]
tags: [HomeLab, security]
pin: true
math: true
mermaid: true
image:
  path: ../assets/img/pfsense-wan-lan-dmz/cover.png
  alt: .
---

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

- Accept copyrigth

![pfsnse-installer-copyrigth](../assets/img/pfsense-wan-lan-dmz/pfsnse-installer-copyrigth.png)

- Set install pfSense

![pfsnse-installer-copyrigth](../assets/img/pfsense-wan-lan-dmz/pfsnse-installer-install.png)

- Select default config

![pfsnse-installer-copyrigth](../assets/img/pfsense-wan-lan-dmz/pfsnse-installer-config.png)

- If we have a raid on our system we select that, on my case i set "Stripe - No Redundancy"

![pfsnse-installer-copyrigth](../assets/img/pfsense-wan-lan-dmz/pfsnse-installer-config.png)

- If we have more than one disk, we need to select where we are going to install all. 

> Select once with "space" key

![pfsnse-installer-copyrigth](../assets/img/pfsense-wan-lan-dmz/pfsnse-installer-zfsconfig.png)

![pfsnse-installer-copyrigth](../assets/img/pfsense-wan-lan-dmz/pfsnse-installer-zfsconfig-2.png)

- Now its time to take some coffe, we probably see somthing like:

![pfsnse-installer-copyrigth](../assets/img/pfsense-wan-lan-dmz/pfsnse-installer-checksum.png)

- Once it ends, we are going to reboot the system.
  
## Config LAN 


On console pfsnse assign automatically ip addreess for a LAN, we are going to set a ip adress.

![pfsnse-installer-copyrigth](../assets/img/pfsense-wan-lan-dmz/config-LAN-setipaddress.png)

![pfsnse-installer-copyrigth](../assets/img/pfsense-wan-lan-dmz/config-LAN-available.png)

![pfsnse-installer-copyrigth](../assets/img/pfsense-wan-lan-dmz/config-LAN-ipv4.png)

![pfsnse-installer-copyrigth](../assets/img/pfsense-wan-lan-dmz/config-LAN-ipv6.png)


>By default all administration is via LAN so we need Enabling Administration via the WAN Interface
> 
>Choose option 8 (Shell) and type **pfctl -d**
>
>This will disable the packet filter entirely and you will be able to access the web interface from any interfaces. Useful for temporary or first time setup.
>
>To enable it back, just type **pfctl -e**

![pfsnse-installer-copyrigth](../assets/img/pfsense-wan-lan-dmz/config-LAN-pfctl.png)

## WIZARD Config

![pfsnse-installer-copyrigth](../assets/img/pfsense-wan-lan-dmz/wizard-config.png)

> Default credentials: username: admin // paswd: pfsense

- Now, we need to configure the pfsense.

![pfsnse-installer-copyrigth](../assets/img/pfsense-wan-lan-dmz/wizard-config-step2.png)

![pfsnse-installer-copyrigth](../assets/img/pfsense-wan-lan-dmz/wizard-config-step3.png)

- On confgure WAN, i set all by default configuration, only i unheck this:

![pfsnse-installer-copyrigth](../assets/img/pfsense-wan-lan-dmz/wizard-config-step4.png)

![pfsnse-installer-copyrigth](../assets/img/pfsense-wan-lan-dmz/wizard-config-step5.png)

- Set a new paswd for admin.

![pfsnse-installer-copyrigth](../assets/img/pfsense-wan-lan-dmz/wizard-config-step6.png)

> If we are connected for wan interface, we need to execute again "pfctl -d" on shell.

And we finish the setUp of pfSense!

> To know that we have everything well configured, if we add a router as an access point to the LAN, or create virtual machines with the vmbr1 (LAN) card, we will see how the traffic flows:
![pfsnse-installer-copyrigth](../assets/img/pfsense-wan-lan-dmz/wizard-config-check.png)

## Config DMZ 

### Proxmos details

- At Proxmox we need to modify the networks

A litle spoiler:
![pfsnse-installer-copyrigth](../assets/img/pfsense-wan-lan-dmz/dmz-proxmox-preview.png)

Install openvswitch-switch on proxmox

```bash
$ apt install openvswitch-switch
```
- Create > OVS Bridge
![pfsnse-installer-copyrigth](../assets/img/pfsense-wan-lan-dmz/dmz-proxmox-ovs-bridge.png)

- Create > OVS inPort


![pfsnse-installer-copyrigth](../assets/img/pfsense-wan-lan-dmz/dmz-proxmox-ovs-inport.png)

 > We can create as many vlans as we want, always associated to vmbr3 in this case.

- We apply the changes, and add this new interface to pfSense.(hardware > Add > network device)

![pfsnse-installer-copyrigth](../assets/img/pfsense-wan-lan-dmz/dmz-proxmox-add-network.png)


### PfSense configuration dmz-pfsense

- Create a vlan

![Alt text](../assets/img/pfsense-wan-lan-dmz/dmz-pfsense-vlan-create.png)
![Alt text](../assets/img/pfsense-wan-lan-dmz/dmz-pfsense-vlan-create-2.png)

>The vlan tag has to be the same as the one we associated in the proxmox, vtnet2 is the new interface we added to pfSense.

- Add new interface to pfsense (vlanDMZ)

![Alt text](../assets/img/pfsense-wan-lan-dmz/dmz-pfsense-assign-vlan.png)

- We activate it and configure it as static ipv4

![Alt text](../assets/img/pfsense-wan-lan-dmz/dmz-pfsense-vlan-config.png)

- Activate the dhcp of this vlan and save (optional, add a range of ips).

![Alt text](../assets/img/pfsense-wan-lan-dmz/dmz-pfsense-vlan-dhcp.png)

### Firewall DMZ

> Firewall > rules

This is very personal because it depends on what rules you want to have, what data flow you want to allow, etc....

In first instance a very basic dmz would be like this: 

- 1º All traffic accepted

![Alt text](../assets/img/pfsense-wan-lan-dmz/dmz-firewall-basic-1.png)

- 2º Block access from the dmz to the LAN
![Alt text](../assets/img/pfsense-wan-lan-dmz/dmz-firewall-basic-2.png)

- 3º We block the passage from the dmz to the wan.
  
![Alt text](../assets/img/pfsense-wan-lan-dmz/dmz-firewall-basic-3.png)

- In the end we will have something like this: 

![Alt text](../assets/img/pfsense-wan-lan-dmz/dmz-firewall-basic.png)


- This is an example of how it could get complicated, feel free to try it out and configure it, stay safe
![Alt text](../assets/img/pfsense-wan-lan-dmz/dmz-firewall-custom.png)

> Now to add machines or create them inside the DMZ we only need the bridge and the tag of our vlan, in this case we only have one vlan which is for the dmz, but we can have several, one for work area, another one for guests, etc...

![Alt text](../assets/img/pfsense-wan-lan-dmz/dmz-example-network.png)

![Alt text](../assets/img/pfsense-wan-lan-dmz/dashboard.png)

> With this you would already have your wifi network separated in WAN/LAN/DMZ 
{: .prompt-tip }





🚀 Don’t forget to check out the 🚀 [DNS & AdBlock](/posts/adblock-configuration/) to improve your PfSense setup.

