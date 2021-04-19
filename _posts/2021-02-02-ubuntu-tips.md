---
layout: posts
title:  "Ubuntu advice"
draft: true
---

## Runlevels

If you want to reboot to a console, just change the default runlevel.  On next boot, it will boot to a console.

`sudo systemctl set-default multi-user.target`

To change back to gui login..

`sudo systemctl set-default graphical.target`

## Holding back upgrades

There are various ways to do this using `dpkg`, `apt` or other commands. These are just some places to start looking.

If there is a specific package that you don't want upgraded, try configuring unattended upgrades:

`/etc/apt/apt.conf.d/50unattended-upgrades`

take a look at the sudo apt policy for the installed package, make note of the installed version:

`sudo apt policy kubernetes`

Take a look at the updates proposed:
```
sudo apt-get clean
sudo apt update
sudo apt list --upgradable
```

Finally, the update frequency must be defined in this file:
`/etc/apt/apt.conf.d/20auto-upgrades`

`sudo apt-mark hold kubectl`
`sudo apt-mark showhold`
