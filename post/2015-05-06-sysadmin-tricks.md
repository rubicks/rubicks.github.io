---
categories:
- posts
date: 2015-05-06T00:00:00Z
title: sysadmin tricks
url: /2015/05/06/sysadmin-tricks/
---

##### Find out which process is listening on some port
###### `netstat`

    $ netstat -tlpn | head -n2
    (Not all processes could be identified, non-owned process info
     will not be shown, you would have to be root to see it all.)
    Active Internet connections (only servers)
    Proto  Recv-Q  Send-Q  Local Address  Foreign Address  State   PID/Program name
    
    $ netstat -tlpn | egrep ":22\b"
    tcp         0       0  0.0.0.0:22     0.0.0.0:*        LISTEN  -
    tcp         0       0  :::22          :::*             LISTEN  -

Here, we print the program names (`-p`)
of those listening (`-l`)
for incoming tcp (`-t`) connections
showing numeric (`-n`) host addresses instead of attempting to determine symbolic host, port, or user names

###### `fuser`

    # fuser 631/tcp
    631/tcp:     7807

Looks like PID 7807 opened tcp port 631.

    # ls -l /proc/7807/exe
    lrwxrwxrwx 1 root root 0 May 11 15:06 /proc/7807/exe -> /usr/sbin/cupsd

PID 7807 is the print server

