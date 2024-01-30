---
title: PfSense DNS and AdBlocker
date: 2024-01-29 22:30:45 +0100
categories: [Network, DNS, adblocker]
tags: [HomeLab, security]
pin: true
math: true
mermaid: true
image:
  path: ../assets/img/pfsense-dns-adblocker/cover.png
  alt: .
---


This configuration is part of [Pfsense-WAN-LAN-DMZ](/posts/network-configuration/), if you want to take a look at it.

---

As now our wifi network is over the LAN, we have control over the packets that are sent and received, that's why we can change the dns and use our own ones like pi-hole, adguard, etc... so that we can filter contents, ads, certain pages, etc...