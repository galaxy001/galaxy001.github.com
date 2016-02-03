---
layout: post
date: 'Wed 2016-02-03 14:09:06 +0800'
slug: "on-dropbox"
title: "On Dropbox"
description: ""
category: 
tags: Galaxy, Tips
---
{% include JB/setup %}

## Linux

### Install

Follow the Gentoo ebuild [net-misc/dropbox/dropbox-3.12.6.ebuild](https://gitweb.gentoo.org/repo/gentoo.git/tree/net-misc/dropbox/dropbox-3.12.6.ebuild).

1. Unpack `dropbox-lnx.x86_64-3.12.6.tar.gz` and move `.dropbox-dist/dropbox-lnx.x86_64-3.12.6/*` to `/opt/dropbox/`.
2. `ldd /opt/dropbox/dropbox` to confirm all `.so` libs are exists at `/lib64/`. Then rm them following:  
````bash
	rm -vf libbz2* libpopt.so.0 libpng12.so.0 || die
	rm -vf libdrm.so.2 libffi.so.6 libGL.so.1 libX11* || die
	rm -vf libQt5* libicu* qt.conf || die
	rm -vf wmctrl || die
	rm -vrf PyQt5* *pyqt5* images || die
	# rm -vf librsync.so.1 || die # 我删除`librsync.so.1`后报错，因为它需要"net-libs/librsync-1"。
	rm -rf library.zip || die # '*.egg'需要保留。
	ln -s dropbox library.zip || die
````
3. `/usr/lib/systemd/system/dropbox@.service`:  
````ini
[Unit]
Description=Dropbox
After=local-fs.target network.target

[Service]
ExecStart=/opt/dropbox/dropboxd
ExecReload=/bin/kill -HUP $MAINPID
KillMode=process
Restart=always
User=%I

[Install]
WantedBy=multi-user.target
````
4. `systemctl`:
````bash
systemctl enable dropbox@galaxy
systemctl start dropbox@galaxy
systemctl status dropbox@galaxy.service
journalctl -xe

systemctl daemon-reload
systemctl reset-failed
````
5. the [Official](http://www.dropboxwiki.com/tips-and-tricks/using-the-official-dropbox-command-line-interface-cli) Dropbox CLI
````bash
wget -O ~/bin/dropbox.py "https://www.dropbox.com/download?dl=packages/dropbox.py"
````
Mirrored [here](/assets/wp-uploads/2016/dropbox.py) due to the GFW.


## Mac