---
layout: posts
title:  "Lab migration notes"
draft: true
---

Having been around network operations people and planning system migrations, I have used VLANs in conversation and understood the concept at a high level but had not had the chance to really dig into the implementations until recently.

## VLANs by design
VLANs need to be defined somewhere by an ID, for example: 42. If a parent organization is defining networks by VLANs, there is already an existing ID. When I plug in a switch to a data center, they tell me what network VLANs they have assigned to me and I configure the switch accordingly. If I want to define my own VLANs, then I would set up a router with 2 interfaces (_inside_ and _outside_), define my own VLAN IDs and tell the switch to keep track of those.

On the switch we can define VLANs in a database.

Per-interface:
 - define a pvid (which is the default) 
 - declare which VLANs to participate in
 - declare which VLANs to tag
 
 ```
interface 0/42
storm-control broadcast level 30
storm-control multicast level 30
description 'You could descibe each interface'
mtu 9216
vlan pvid 42
vlan participation include 42,203
vlan tagging 203
exit
```

So in this example, a system plugging into the switch on port 42, would default participate in the 42 VLAN. Additionally (within the OS) an a VLAN interface could be defined to communicate on 203 vlan.

### How can I see who is communicating on which VLAN?

From the switch, there may be a command to show the mac address table (`show mac-addr-table`). Entries expire quickly, so you may need to run it a few times to get a sense of which MAC addresses are talking on which VLANs.

Another way to see, is to query the network neighbor cache using `arp -an` (after doing something like `nmap`).

## DHCP (Why configure each server?)

Install the service on Ubuntu using apt:

`sudo apt install isc-dhcp-server`

Edit the configuration file:

`vim /etc/dhcp/dhcpd.conf`

Some useful settings would be the range of IP addresses to give out for each subnet, the default gateway, DNS and NTP servers. 

In Ubuntu 20, you will need to specify the interface (in [two places](https://askubuntu.com/a/1275120/1095652)).

**Note:** _the settings are slightly different for publicly routable addresses_

Finally `sudo service isc-dhcp-server restart` to apply the configuration.

There are several [communtity](https://help.ubuntu.com/community/isc-dhcp-server) [guides](https://devtutorial.io/how-to-setup-dhcp-server-in-ubuntu-server-20-04.html) and [references](https://ubuntu.com/server/docs/network-dhcp) around on this [topic](https://ubuntu.com/server/docs/network-dhcp), but they all seem really simple (but nothing is as authoritative as the [ISC page on DCHP](https://www.isc.org/dhcp/).

**Note:** _seeing DHCPDISCOVER/DHCPOFFER, but no DHCPACK could mean that a misconfiguration with [DHCP snooping](https://packetpushers.net/five-things-to-know-about-dhcp-snooping/) is intercepting the client server conversation.**_

