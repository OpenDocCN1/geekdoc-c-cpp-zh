The output in Example 26-4 was taken from Router R1 as shown in the earlier examples, after doing some testing from the NMS at address 10.1.3.3. The highlighted items point out the number of SNMP packets received (input) and sent (output), as well as the number of requested MIB variables—that is, the number of variables requested in different SNMP Get requests. (Note that SNMP also supports the GetNext and GetBulk commands, so a single NMS user click can cause the NMS to Get many variables from an agent; thus, it is not unusual for the requested variables counter to get very large.) The output also shows that seven Set requests were received, resulting in two changes to variables. The fact that two Set requests changed variables is a good fact to know if you are wondering if someone has reconfigured something on the device using SNMP.

# Implementing SNMP Version 3

SNMPv3 configuration on Cisco routers and switches has some commands in common with SNMPv2c configuration, and some completely different commands. The configuration to support sending Traps and Informs, using the snmp-server host and snmp-server enable traps commands, works almost identically, with a few small differences. However, SNMPv3 replaces all references to communities, and as a result does not use the snmp-server community command at all. Instead, it uses the snmp-server group and snmp-server user commands to configure the security features available to SNMPv3.

SNMPv3 has many more configuration options, and it is easy to get confused by the details. So, to get started, first look at a short SNMPv3 configuration example, as shown in Example 26-5. The example highlights the values you would have to choose, but the values are either text fields (names and passwords) or the IP address of the NMS. This configuration could be used to replace the SNMPv2c configuration and use username/password authentication. The requirements met in the example are

+   - Use SNMPv3 authentication (basically replacing SNMPv2 communities).
+   - Use username Youdda and authentication password madeuppassword (in your network, you would choose your own values).
+   - Do not use SNMPv3 privacy (that is, message encryption).
+   - Allow both read (Get) and write (Set) access.
+   - Send Traps to an NMS (10.1.3.3), authenticating with the same username.

Example 26-5 Configuring SNMPv3 on R1—Authentication Only

```
```
R1(config)# snmp-server group BookGroup v3 auth write v1default
R1(config)# snmp-server user Youdda BookGroup v3 auth md5 madeuppassword
R1(config)# snmp-server host 10.1.3.3 version 3 auth Youdda
```
```

Given the list of requirements, you could probably just read the configuration in Example 26-5, compare that to the list of requirements preceding the example, and correctly guess what most of the command parameters mean. However, we need to get into more detail to work through these commands and their options so that you understand the entire configuration, which is exactly what the next few pages do.