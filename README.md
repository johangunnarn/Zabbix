# Zabbix
Zabbix repository for Zabbix templates mainly focused on networking

Feel free to use the templates, if you have any questions you can contact me on Discord, my username is: stickan

Originally forked from https://github.com/flaviojunior1995/Zabbix

# Template_Cisco-BGP_SNMP.xml

Tested on Cisco ASR 9901

To resolve OID to IPv6 address correctly, you need to install the external script [oid_to_ipv6](https://github.com/johangunnarn/Zabbix/blob/main/External_Scripts/oid_to_ipv6)

Items:
* Amount of accepted prefixes from neighbor
* Administrative status for neighbor
* ASN Name for neighbor
* Last received error for neighbor
* Established time with neighbor
* Configured max prefix for neighbor
* Status for neighbor
* Remote AS for neighbor
* OID to IPv6 Address from neighbor

Triggers:
* If uptime is low for neighbor (default 3600 seconds)
* If neighbor is close to reaching configured max prefix limit and has a warning value
* If neighbor is down

Graphs:
Currently only IPv4 amount of prefixes accepted

# Template_Yeti_SEMS.xml

Uses yeti-cmd to get items, commands found [here](https://yeti-switch.org/docs/en/yeti-cli/commands.html)

You'll need package "jq" installed and the following user parameters in zabbix_agentd.conf of agent server:
```
UserParameter=sems.calls.count,yeti-cmd 127.0.0.1 yeti.show.calls.count
UserParameter=sems.service.state,systemctl is-active sems.service
UserParameter=sems.yeti.version,yeti-cmd 127.0.0.1 yeti.show.version | jq -r '.build'
UserParameter=sems.sems.version,yeti-cmd 127.0.0.1 core.show.version | jq -r '.core_build'
```

Items:
* Amount of calls currently on SEMS node
* Status of service sems
* Version of yeti
* Version of sems

Triggers:
* If sems service is not running (inactive)
