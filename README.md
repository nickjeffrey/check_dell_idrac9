# check_dell_idrac9
nagios check for Dell iDRAC 9 service processors

# Requirements
perl, snmpget on nagios server, SNMP enabled on iDRAC service processor

# Configuration

Enable SNMP on the iDRAC service processor
<img src=images/idrac9_snmp.png>

You will need a section in the services.cfg file on the nagios server that looks similar to the following.
```
    # Define a service to check the Dell iDRAC service processor
    # Parameters are SNMP community name
    define service {
       use                             generic-service
          hostgroup_name               all_dell_idrac9
          service_description          iDRAC
          check_command                check_dell_idrac9!public
          }
```

You will also need a command definition similar to the following in commands.cfg on the nagios server
```
    # 'check_dell_idrac9' command definition
    # parameters are -H hostname -C snmp_community
    define command{
       command_name    check_dell_idrac9
       command_line    $USER1$/check_dell_idrac9 -H $HOSTADDRESS$ -C $ARG1$
       }
```

# Output
You should see output similar to the following
<img src=images/idrac9.png>
