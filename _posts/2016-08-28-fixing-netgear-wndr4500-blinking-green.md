---
layout: post
title: Fixing Netgear WNDR4500 Blinking Green Power Light (Corrupted Firmware)
date: '2016-08-28T12:55:00.000-05:00'
author: Josh Kendrick
tags:
- wndr4500
- network
- netgear
- osx
---

**I had this happen to me again the other day and revisited [my original blog post]({{ site.url }}/2014/05/10/fixing-netgear-wndr4500-blinking-green/) to fix it. I realized the original blog post had some broken links and needed some love, so I'm posting it again with tweaks.**

I realized there was an issue when my router's power button was blinking instead of solid, and I could no longer access it at the static IP I had set.

So I Googled and found ~~[a link on kb.netgear.com](http://kb.netgear.com/app/answers/detail/a_id/18989/~/router-power-led-blinks-slowly-and-router-no-longer-works)~~(link doesn't work anymore) that seemed like it was going to be a huge help. Basically, the power flicker caused the router's firmware to become corrupted, so I would have to reload the firmware myself. However, I was doing this on a Mac (specifically OS X 10.9 Mavericks), and there a few issues I ran into. I’ve posted the steps from the above article here, in case it disappears, and have included the workarounds for doing this on my Mac.

1. **Download the latest router firmware to your computer**. If you search for WNDR4500 on [this page](http://support.netgear.com/for_home/default.aspx), it should [send you here](http://support.netgear.com/product/wndr4500#wrapper), where you can see a link for the firmware on the right. I've linked [the latest version I found as of this writing]({{ site.url }}/assets/WNDR4500-V1.0.1.40_1.0.68.zip).

2. **You'll need a tftp client**. OS X already has one installed.

3. **Connect your laptop/computer to the router via an ethernet LAN port on the back**. I also turned off any wi-fi or other connections from that laptop/computer, but I'm not sure that's necessary. I just wanted to be sure I was only talking to that router

4. **Configure the computer with a static IP address of 192.168.1.2 and a subnet mask of 255.255.255.0**
    - On OS X open up System Preferences > Network, and you want to find your ethernet connection in the box on the left. If you turned off all other connections on that computer, it should be the only connection with a green dot. In the drop down for Configure IPv4, change it to Manually. Set the IP Address and Subnet Mask like above, and you can leave router empty.
    - (When you're done with everything here and want to put it back, you can set it back to just DHCP).

5. You'll need to push the firmware and that was the part that gave me the most trouble. I had to Google around a bit to figure out how to tftp the file. Here are those instructions for OS X:
    - **Unzip the downloaded firmware someplace** (it should be a zip file)
    - **Open Terminal and cd to inside the unzipped directory**. This is very important. Later, when you go to put the file from the tftp prompt, it will not work unless you started the tftp prompt from the same directory as the .chk file.
    - **Type `tftp -e 192.168.1.1` into the terminal** NOTE: The -e is really important! I tried it a few times without the -e and was thinking it just wasn't going to work. But after looking in the App tftp man pages, I found: '-e sets a binary transfer mode', meaning it is needed so that the file is transferred byte by byte. The router will not install the firmware if you tftp without the -e option. (I believe the PC equivalent is -i?).
    - Then on the tftp prompt you get back, **type `put <name-of-file>`**. It should look like: `put WNDR4500-V1.0.1.40_1.0.68.chk`.
    - tftp should report back successful and how long it took. Shortly after, you should notice the lights on your router doing things. It is installing and restarting.

6. **This isn't necessary:** ~~Wait a few minutes, and reboot the router. On this model there's a handy power button on the back you can push in and push in again to turn it off then on.~~

7. **This _might_ be necessary:** After that you'll need to reset the router by pressing in the reset button on the back for at least 30 seconds.

8. At this point you'll want to **set your computer's ip address back to DHCP**.

9. **Only necessary/true if you did step 6:** Then, you should be able to **go to `192.168.1.1` and log in with `username: admin, password: password`**.
    - You will have to **reconfigure the router back to the way you had it**.

Hope that helps someone!
