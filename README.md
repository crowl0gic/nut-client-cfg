# NUT v2.8.0 Client Config
Tested on Debian Bullseye 11 and Ubuntu 20.04

## Prerequisites
Please review [NUT Server Config](https://github.com/crowl0gic/nut-server-cfg) before proceeding with this document 

## Introduction 
The NUT client processes power events that are broadcast from the NUT server and shuts down the host where it is installed. It may also issue commands to the NUT server (depending on permissions granted in /etc/nut/upsd.users on the server). The client does not require SNMP drivers. 

## Binaries
```
├── bin
│   ├── upsc
│   ├── upscmd
│   ├── upslog
│   ├── upsrw
│   └── upssched-cmd
├── dep
│   └── libupsclient.so.6.0.0
├── lib
│   └── upsmon
└── sbin
    └── upssched
```

## Configuring the NUT Client

### /etc/nut/nut.conf
Should contain `MODE=netclient`

### /etc/nut/upsmon.conf
1. Define which UPS(es) you will be monitoring here
2. `MINSUPPLIES` will probably be 1
3. You can use a `SHUTDOWNCMD` similar to `SHUTDOWNCMD "/usr/bin/logger fake shutdown command"` to speed up your testing process
4. Define the `NOTIFYCMD` and `NOTIFYFLAG`s that will be used (varies by driver / UPS capabilities). 

### /etc/nut/upssched.conf
Determines what occurs at specific UPS events. Sets the shutdown timer that will be used to shut off the host and complement processes.

Be sure to uncomment the `CMDSCRIPT` and `PIPEFN` parameters and set appropriate paths

The timer you configure here determines when the client will shutdown. It's important to ensure that your shutdowns are synchronized!

