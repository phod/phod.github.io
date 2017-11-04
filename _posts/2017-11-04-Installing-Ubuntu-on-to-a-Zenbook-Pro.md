---
layout: post
title: Installing Ubuntu 16.04 on an Asus Zenbook Pro UX550
---

** IN PROGRESS **

I just got my Ubuntu installation finished on my Zenbook. For the most part
I could just follow other guides, but there were a few things that had to be done.

Preface: I encountered some issues installing Ubuntu onto my laptop. If you're able to
install a newer version of Ubuntu immediately, then go for it. However, I was unable to 
get to the installer, even when following guides here.

Ingredients:

- 2 USB memory sticks
- An external keyboard (Optional)
- An ethernet to USB adapter

## Step 1: Preparation

1. Make a windows backup disk. You want this. Seriously. Just in case you successfully break
everything, having this is a nice reset button. You can read here for information:

2. Download Ubuntu. For my laptop I ran into issues with 17.10 and 16.04. But had some luck with the
14.04 installer. Your milage may vary. Download Rufus and burn Ubuntu onto
your other USB memory stick.

## Step 2: Shrinking the Windows partition

Skip this if you're replacing Windows entirely. But I wanted to keep my Windows
partition around just in case. And it's not much extra work if you're willing to
sacrifice a little bit of your storage.

1. Make a windows backup disk. You want this. Just in case you successfully break
everything, having this is a nice reset button. You can read here for information:

2. Shrink your partition. This is unfortunately going to be a bit more work than
just shrinking the windows partition. Give it a go, but you'll likely have
some unmoveable files. For the most part you can follow the guides here. The only
catch was that I had to configure the swap size in the UI and manually delete some
restore points that had already been created. Follow instructions here: <link>

You shouldn't need to install any 3rd party software, but if it gets tough you can
try something, unfortunately I cannot recommend any, so you'll need to do your
own research.

Once you've shrunk your partition you're ready to install Ubuntu.

## Step 3: Installing Ubuntu

I encountered some issues when trying to following this guide <> to install
Ubuntu 16.04 immediately. Specifically, when trying to modify the Grub settings,
my 'p' key would register as '*'. I spent some time trying to figure out how I could
programatically get around this, until I discovered my ')' key had a similar issue.
I managed to work around this with my external keyboard (model) being recognised
correctly. However, I was consistently stuck with CPU locking and never starting
the 16.04 installer. So I had to give up on 16.04. I was running into similar issues with 17.10,
but didn't give it as much time. So it may have been resolvable.

Next I tried 14.04. This did boot. Sometimes the trackpad doesn't work, rebooting seems
sufficient to fix this. But an external mouse may also work. Even with my ethernet
plugged in I couldn't get the installer to recognise my internet connection. So
I had to resolve some stuff afterwards.

Go through the Ubuntu installation flow. You should have 14.04 working.

Next we need to get up to date again! You should see Ethernet is working now. However
WiFi was not. It turns out I need Linux kernel 4.10+ for WiFi support. 14.04 gives you
4.4. I couldn't find any evidence of Ubuntu 14.04 playing well with the 4.10 linux
kernel. But we can do an upgrade to 16.04 and be okay.

This step is likely unnecessary. However do a quick apt-get update and apt-get upgrade and apt-get
dist-upgrade (Ubuntu installer will prompt you to do this anyways).

Now begin the process of upgrading Ubuntu to 16.04: <link>

Once you have Ubuntu 16.04 installed, you should be able to install the
4.10 kernel with <commands>. Reboot and WiFi should now be working.

At this stage I was happy to pause on configuration. I wanted to start development on
my laptop.

Things to to:
- The speakers misbehave. They are either 0% or 100%. No inbetween.
- Upgrade Ubuntu to 17.10.
- Battery pluggin in doesn't update icon to say charging.
