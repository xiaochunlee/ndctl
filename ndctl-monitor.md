---
title: ndctl
layout: pmdk
---

NAME
====

ndctl-monitor - Monitor the smart events of nvdimm objects

SYNOPSIS
========

>     ndctl monitor [<options>]

DESCRIPTION
===========

Ndctl monitor is used for monitoring the smart events of nvdimm objects and dumping the json format notifications to syslog, standard output or a logfile.

The objects to monitor and smart events to notify can be selected by setting options and/or the default configuration file (/etc/ndctl/monitor.conf). Both of the values in configuration file and in options will work. If there is a conflict, the values in options will override the values in configuration file. The changed values in configuration file will work after the monitor is restarted.

EXAMPLES
========

Run a monitor as a daemon to monitor DIMMs on bus "nfit\_test.1"

>     ndctl monitor --bus=nfit_test.1 --daemon

Run a monitor as a one-shot command and output the notifications to /var/log/ndctl.log

>     ndctl monitor --log=/var/log/ndctl.log

Run a monitor daemon as a system service

>     systemctl start ndctl-monitor.service

OPTIONS
=======

`-b; --bus=`  
Enforce that the operation only be carried on devices that are attached to the given bus. Where *bus* can be a provider name or a bus id number.

`-d; --dimm=`  
A *nmemX* device name, or dimm id number. Select the devices to monitor reference the given dimm.

`-r; --region=`  
A *regionX* device name, or a region id number. The keyword *all* can be specified to carry out the operation on every region in the system, optionally filtered by bus id (see --bus= option).

`-n; --namespace=`  
A *namespaceX.Y* device name, or namespace region plus id tuple *X.Y*.

`-l &lt;file | syslog | standard&gt;; --log=&lt;file | syslog | standard&gt;`  
Send log messages to the specified destination.

`<file>`  
Send log messages to specified &lt;file&gt;. When fopen() is not able to open &lt;file&gt;, log messages will be forwarded to syslog.

syslog  
Send messages to syslog.

standard  
Send messages to standard output.

The default log destination is *syslog* if "--daemon" is specified, otherwise *standard*. Note that standard and relative path for &lt;file&gt; will not work if "--daemon" is specified.

`-c; --config-file=`  
Provide the config file to use. This overrides the default config typically found in /etc/ndctl/

`--daemon`  
Run a monitor as a daemon.

`-D; --dimm-event=`  
Name of an smart health event from the following:

-   "dimm-spares-remaining": Spare Blocks Remaining value has gone below the pre-programmed threshold.

-   "dimm-media-temperature": NVDIMM Media temperature value has gone above the pre-programmed threshold.

-   "dimm-controller-temperature": NVDIMM Controller temperature value has gone above the pre-programmed threshold.

-   "dimm-health-state": NVDIMM Normal Health Status has changed

-   "dimm-unclean-shutdown": NVDIMM Last Shutdown Status was a unclean shutdown.

The monitor will attempt to enable the alarm control bits for all specified events.

`-u; --human`  
Output monitor notification as human friendly json format instead of the default machine friendly json format.

`-v; --verbose`  
Emit extra debug messages to log.

COPYRIGHT
=========

Copyright (c) 2018, FUJITSU LIMITED. License GPLv2: GNU GPL version 2 <http://gnu.org/licenses/gpl.html>. This is free software: you are free to change and redistribute it. There is NO WARRANTY, to the extent permitted by law.

SEE ALSO
========

[ndctl-list](ndctl-list.md), [ndctl-inject-smart](ndctl-inject-smart.md)