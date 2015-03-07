wagwan
========
###### Generates a friendly status report from **op5 Monitor**

Overview
========
*wagwan* uses *op5 Monitor's* REST API to extract information to used to create a compact status report.   
This report includes information about helath of hosts, the amount of notifications sent out and similar.   

Current features
========
- Enterprise ready greeting and error messages
- Ability to exclude hosts or host groups from report 
- Get the current over-all status of your hosts
- Get number of recieved log messages and some historical comparison'
 
Feature wish list 
=================
- Base reports on objects with specific contact group
- Devliver report in JSON and other formats
- Support Icinga2's REST API

Installation and usage example
==============================
The script uses nothing outside the Python 2.7 standard library, except the "requests" module.  
If you want to use *wagwan* on EL6, you will need to install the "argparse" module as well.   

The command below will generate a report with host names matching "test-" and host group "Windows servers" excluded.   
It will also send application logs to syslog and pipe the output to the "smssend" utility:   

```
$ ./wagwan.py --server 'mon.i.tor' --username 'read_only_1' --password 'god' --exclude-host 'test-.*' --exclude-host-group 'Windows servers' --logging syslog | smssend 46730000000
-- 
Text: Hey man - what's up?
Out of 17 hosts, 8 are up, 3 have had problems acknowledged,
2 are unreachable and 4 are down - you might wanna take a look at that.
During the last 24 hours we recieved 3305 log messages - that's 451 more than the previous day!

Cya around, mate
To: 46700000000
```
