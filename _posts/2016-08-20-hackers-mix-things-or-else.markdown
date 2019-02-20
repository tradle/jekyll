---
layout: post
title: Hackers mix things, or else
image: "/content/images/2016/08/photo-1452802447250-470a88ac82bc.jpeg"
date: '2016-08-20 22:30:00'
tags:
- docker
- mac
- errors
- dev-environment
- technical
---
![](/content/images/2016/08/photo-1452802447250-470a88ac82bc.jpeg)
I just switched from using Docker Toolbox to [Docker for Mac](https://docs.docker.com/docker-for-mac/).

Docker for Mac, wait for it....is only for Macs, because it uses [HyperKit](https://github.com/docker/hyperkit) instead of VirtualBox, and HyperKit only supports OSX at the moment.

I pulled the plug on Docker Toolbox for two reasons:

1. Android Emulator bitched to me regularly about VirtualBox not letting it emulate things.

  > emulator: ERROR: Unfortunately, VirtualBox 4.3.30+ does not allow multiple hypervisors to co-exist. In order for VirtualBox and the Android Emulator to co-exist, VirtualBox must change back to shared use. Please ask VirtualBox to consider this change here: https://www.virtualbox.org/ticket/14294

  So no running Docker and the Android Emulator at the same time. One more to add to the list:
  - don't pour water into acid
  - date a nice Jewish girl (too late)
  - ...
  - don't use heroin to cure cocaine addiction ([the Knick](http://www.imdb.com/title/tt2937900/) anyone?)
  - don't run Docker and Android Emulator together

  No self respecting adult follows the above rules. Go ahead, tell a hacker not to mix things, I dare you.

2. I swear, I had two reasons when I started...

Sadly, my joy was pre-mature. The new error is:

> emulator: ERROR: Unfortunately, there's an incompatibility between HAXM hypervisor and VirtualBox 4.3.30+ which doesn't allow multiple hypervisors to co-exist.  It is being actively worked on; you can find out more about the issue at http://b.android.com/197915 (Android) and https://www.virtualbox.org/ticket/14294 (VirtualBox)
Internal error: initial hax sync failed

Hilariously enough, after uninstalling VirtualBox, and restarting my Mac, the same error persists. If anyone has had better luck, please comment. (Simon, can we get some commenting support on this blog?).
