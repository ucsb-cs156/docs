---
parent: CSIL
grand_parent: Topics
layout: default
title: "CSIL: Via MacOS"
description:  "Accessing CSIL from your MacOS system"
indent: true
---

# Accessing CSIL from MacOS

To access CSIL from MacOS, you can use the Terminal command, and type the following, replacing `cgaucho` with your ECI/CSIL username:

```
ssh cgaucho@csil.cs.ucsb.edu
```

NOTE: For Fall 2020, we are asked to no longer use `csil-01 through csil-48`, but only `csil.cs.ucsb.edu`.  This is a change from previous quarters.

# What about the `no $DISPLAY environment variable` error?

If  try to run a program that uses a Java GUI, or any other type of graphics window,
and you get this message:

```
no display name and no $DISPLAY environment variable
```

then there are two options:

1.  Use the Remote Desktop option (see below)
2.  Use X11 with XQuartz (see below)(though ECI notes that X11 is deprecated as of Fall 2020)

then you need to install XQuartz as explained below, log out, log in, and try again.

# Connecting with Remote Desktop

With this option, you have a window on your local computer that shows the entire Linux Desktop on the remote machine.  It is different from the X11 options we used in the past.

Instructions for connecting to CSIL via Remote Desktop appear here: 
* <https://doc.engr.ucsb.edu/display/EPK/Remote+Access+to+Computer+Science+Computing+Labs>
* MacOS specific instructions are here: <https://doc.engr.ucsb.edu/display/EPK/CS+Lab+RDP+Access+-+MacOS+Client>
* You will also need the Campus VPN Client (Pulse Secure) which you can install here: <https://dev-it-ucsb-edu-v01.pantheonsite.io/get-connected-vpn/pulse-secure-vpn-client-mac-os>


# Using Samba with MacOS

Another option is to mount your CSIL home directory *as if* it were a local directory on your Mac.

This allows you, for example, to edit files on CSIL using VSCode running on your Mac.

To do this, see the instructions here: <https://doc.engr.ucsb.edu/pages/viewpage.action?pageId=3342386>




