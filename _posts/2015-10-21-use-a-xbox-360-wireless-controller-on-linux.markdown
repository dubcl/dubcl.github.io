---
layout: post
title: Use a Xbox 360 wireless controller on Linux
date: '2015-10-21 03:35:51'
---

I love play games since I was child, I remember escape from school to go to the arcades XD.

Actually I have many games, consoles, arcade parts, etc, one day I post about that ;), and one of that game parts is a Hori Tekken 6 wireless fighting stick for Xbox 360, like this:

![](http://ecx.images-amazon.com/images/I/41DjUNDmKHL._SX425_.jpg)

To configure on Linux, we need a "wireless receiver for windows" like this, (yes, the same ;) )

![](http://i.ebayimg.com/00/s/MjU0WDMwMA==/z/vpwAAOSw6EhUNbza/$_35.JPG)

And do this on our system as root:

```language-bash
rmmod xpad
```
If you want, you can add a blacklist for the module, do as root:

```language-bash
echo "blacklist xpad" > /etc/modprobe.d/xpad.conf
```

Then we need install xboxdrv

```language-bash
apt-get install xboxdrv
```

Once done we can connect the wireless receiver and execute this as you normal user:

```language-bash
sudo xboxdrv -s --trigger-as-button --type xbox360
```

Now you can synchronize you devices with you receiver like you do with your Xbox 360.

That's all, too easy, this work with any Xbox 360 wireless device, and up to 4 devices at the time, for play TMNT or Sunset Riders on mame with 4 players hehehehe.

More info:

http://pingus.seul.org/~grumbel/xboxdrv/xboxdrv.html
https://github.com/xboxdrv/xboxdrv
