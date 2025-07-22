# check_aix_snmp
nagios check for AIX SNMP daemons

# Requirements
perl, snmpget|snmpinfo on nagios server

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
