---
title: "SQL - basic commands"
date: 2020-02-04
draft: false
diagram: false
tags: [shell, bash]
slug: bash-p1-basics
toc: true
weight: 40
summary: basic bash commands
---

## Show tables

```bash
sqlite>.tables
users
```

## System info

```bash
#!/bin/bash

# Show shell name.
echo $SHELL
echo $0
# Show shell version.
$SHELL --version

# Clear terminal.
clear

# Show command history.
history

# Print working directory
pwd

# Show system info
uname -a

# uptime
uptime
```

## File managing

```bash
#!/bin/bash

# List the files in working directory.
ls
# List all files, hidden file included, with detailed information.
ls -la
```

## Network

```bash
#!/bin/bash

# Show network interface config/info.
ifconfig

# get public ip
curl icanhazip.com

# Show network status
netstat
# Show all, include tcp/udp port.
netstat -an
# Show established connection
netstat -antu | grep 'ESTABLISHED'
# Show kernel routing information
netstat -r
netstat -tulnp

# Check the bridge Interface
brtcl
brctl addbr <name>

# ssh
ssh
# Generate a new ssh-key. Usually used when attempt to ssh a address which has change device/remote host. Use this when encounter error message: WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!
ssh-keygen

# scp
scp
```

## CPU, memery, task & process

### Check and monitor process

```bash
#!/bin/bash

# List all process run by user shell
ps
# List all process, even by status
ps aux
# pstree
pstree

# Monitor the process status
top
# cpu
top -o cpu
# memery
top -o rsize

# List cronjob
crontab
# List all cronjob.
crontab -l
```

### Sending signal or kill process

```bash
#!/bin/bash

# Send a signal to a process
kill -signal PID
# Send 15 SIGTERM to a process
kill $pid

# killall allow you to kill app with name instead of pid
killall -9 $processname
# Ask before terminate
killall -i -9 $processname
```

### Memory usage

```bash
#!/bin/bash

# Show recent memory usage
free -m
```

## References

- <https://geekflare.com/netstat/>
- <http://linux.vbird.org/linux_basic/0440processcontrol.php#ps_l>
