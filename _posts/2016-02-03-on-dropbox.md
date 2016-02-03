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

* Unpack `dropbox-lnx.x86_64-3.12.6.tar.gz` and move `.dropbox-dist/dropbox-lnx.x86_64-3.12.6/*` to `/opt/dropbox/`.
* `ldd /opt/dropbox/dropbox` to confirm all `.so` libs are exists at `/lib64/`. Then rm them following:

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

#### For **systemd**

* `/usr/lib/systemd/system/dropbox@.service`:

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
* `systemctl`:

````bash
systemctl enable dropbox@galaxy
systemctl start dropbox@galaxy
systemctl status dropbox@galaxy.service
journalctl -xe

systemctl daemon-reload
systemctl reset-failed
````
* the [Official](http://www.dropboxwiki.com/tips-and-tricks/using-the-official-dropbox-command-line-interface-cli) Dropbox CLI

````bash
wget -O ~/bin/dropbox.py "https://www.dropbox.com/download?dl=packages/dropbox.py"
````
Mirrored [here](/assets/wp-uploads/2016/dropbox.py) due to the GFW.

#### for **OpenRC**

* `/etc/init.d/dropbox`

````bash
#!/sbin/runscript
# Copyright 1999-2014 Gentoo Foundation
# Distributed under the terms of the GNU General Public License, v2 or later
# $Id$

depend() {
	need localmount net
	after bootmisc
}

start() {
	local tmpnice="${NICE:+"--nicelevel "}${NICE}"
	local tmpionice="${IONICE:+"--ionice "}${IONICE}"
	local started=""

	ebegin "Starting dropbox"
	for dbuser in ${DROPBOX_USERS}; do
	local homedir=$(eval echo ~${dbuser})
	if test -d "${homedir}" && \
		echo 0 > ${homedir}/.dropbox/dropbox.pid && \
		start-stop-daemon -S -b \
		${tmpnice} ${tmpionice} \
		-u ${dbuser} -v \
		-p ${homedir}/.dropbox/dropbox.pid \
		-e HOME=${homedir} \
		-x /opt/bin/dropbox; then
		started="${started} ${dbuser}"
	else
		eend $?
		eerror "Failed to start dropbox for ${dbuser}"
		if [ -n "${started}" ]; then
		eerror "Stopping already started dropbox"
		DROPBOX_USERS=${started} stop
		fi
		return 1
	fi
	done
	if [ -z "${started}" ];then
	eerror "No dropbox started"
	eend 1
	else
	eend 0
	fi
}

stop() {
	local retval=0
	ebegin "Stopping dropbox"
	for dbuser in ${DROPBOX_USERS}; do
	local homedir=$(eval echo ~${dbuser})
	start-stop-daemon --stop \
		--pidfile ${homedir}/.dropbox/dropbox.pid || retval=$?
	done
	eend ${retval}
}

status() {
	for dbuser in ${DROPBOX_USERS}; do
	local homedir=$(eval echo ~${dbuser})
	if [ -e ${homedir}/.dropbox/dropbox.pid ] ; then
			echo "dropboxd for USER $dbuser: running."
	else
			echo "dropboxd for USER $dbuser: not running."
	fi
	done
}
````

* `/etc/conf.d/dropbox.conf`

````bash
# /etc/conf.d/dropbox.conf: config file for /etc/init.d/dropbox

# Users to run dropbox
DROPBOX_USERS=""

# integer [-20 .. 19 ] default 0
# change the priority of the server -20 (high) to 19 (low)
# see nice(1) for description
#NICE=0

# See start-stop-daemon(8) for possible settings
#IONICE=2

PID_DIR=/var/run/dropbox
````


## Mac