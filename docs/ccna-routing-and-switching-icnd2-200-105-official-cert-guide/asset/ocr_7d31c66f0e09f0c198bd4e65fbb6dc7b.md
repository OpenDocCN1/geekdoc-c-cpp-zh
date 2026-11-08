> **NOTE** IOS allows you to reconfigure the `snmp-server user` command so that it omits the auth or priv keyword, even when the referenced `snmp-server group` command uses the auth or priv parameter. However, that misconfiguration causes the SNMP agent to not be able to communicate with the SNMP manager. For instance, if the `snmp-server user` command omits the auth keyword and associated parameters, but the `snmp-server group` command uses the auth keyword, IOS accepts the configuration commands, but authentication fails when the agent and NMS try to communicate.

Example 26-7 shows a series of **snmp-server group** and matching **snmp-server user** commands, one after the other, so you can more easily see the parameters. Note that the **snmp-server group** commands do not include the optional parameters to enable writes (write v1 default) or to use an ACL, just to reduce clutter.

# **Example 26-7**  *SNMPv3 Configuration Samples: Groups and Users*

```
```text
! The group uses noauth, so the user Youdda1 has no auth nor priv keyword
snmp-server group BookGroup1 v3 noauth
snmp-server user Youdda1 BookGroup1 v3

! The next group uses auth, so the next two users use the auth keyword, but not priv
snmp-server group BookGroup2 v3 auth
snmp-server user Youdda2 BookGroup2 v3 auth md5 AuthPass2
snmp-server user Youdda3 BookGroup2 v3 auth sha AuthPass3

! The next group uses priv, so the next users use both the auth and priv keywords.
snmp-server group BookGroup3 v3 priv
snmp-server user Youdda4 BookGroup3 v3 auth md5 AuthPass4 priv des PrivPass4
snmp-server user Youdda5 BookGroup3 v3 auth md5 AuthPass3 priv 3des PrivPass5
snmp-server user Youdda6 BookGroup3 v3 auth sha AuthPass3 priv aes 128 PrivPass6
```
```

Note that the example also shows samples of several authentication and encryption options, as listed in Figure 26-9.

# Verifying SNMPv3

Verifying SNMPv3 operation begins with confirming the details of the SNMPv3 configuration. You can of course find these with the **show running-config** command, but two commands in particular repeat the configuration settings. Example 26-8 shows the output from one of those commands, **show snmp user**, taken from Router R1 after adding the configuration listed in Example 26-7.

# **Example 26-8**  *Verifying SNMPv3 Configuration Settings*

```
```text
R3# show snmp user
User name: Youdda1
Engine ID: 800000090300D4C8B57D8200
storage-type: nonvolatile        active
Authentication Protocol: None
Privacy Protocol: None
```
```