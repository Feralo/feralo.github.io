---
layout: posts
title:  "Ubuntu advice"
---

If you want to reboot to a console, just change the default runlevel.  On next boot, it will boot to a console.

`sudo systemctl set-default multi-user.target`

To change back to gui login..

`sudo systemctl set-default graphical.target`
