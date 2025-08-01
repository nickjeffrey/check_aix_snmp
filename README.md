# check_aix_snmp
nagios check for AIX SNMP daemons

# Requirements
perl, snmpget on nagios server

# Configuration

This script is executed on the nagios server, and queries a remote AIX host to confirm the AIX SNMP daemons are running

You will need a section in the services.cfg file on the nagios server that looks similar to the following.

```
    # Define service to peform SNMP queries against remote AIX machine to confirm AIX SNMP daemons are running
    # Pass the SNMP community string as the only parameter
    define service {
       use                             generic-24x7-service
       hostgroup_name                  all_aix,all_vio
       service_description             AIX SNMP
       check_command                   check_aix_snmp!public
       }
```


You will also need a command definition similar to the following in the commands.cfg file:
```
    # check_aix_snmp command definition
    # adjust SNMP community name as appropriate
    define command{
       command_name    check_aix_snmp
       command_line    $USER1$/check_aix_snmp --community=$ARG1$ --host=$HOSTADDRESS$
       }
                                                                                  
```

# Sample Output
```
AIX SNMP OK -- SNMP response from aixhost.example.com on .1.3.6.1.4.1.2.3.1.2.2.2.1.1.1.1.1
```
```
AIX SNMP CRITICAL -- no SNMP response from aixhost.example.com on .1.3.6.1.4.1.2.3.1.2.2.2.1.1.1.1.1.    This is the AIX MIB.  Confirm $hostname runs AIX, and the relevant section is uncommented from /etc/snmpdv3.conf
```
