In other words, remote and local zones must be configured on the gatekeeper. The outvia keyword is used to determine if a local Cisco UBE is available for processing the call. To configure remote zones, use commands like the following:

```
Router1> enable
Router1# configure terminal
Router1(config-gk)# zone remote spGK spname 10.16.193.158 1719 invia myGK outvia myGK
Router1(config-gk)# exit
```

The key command is the zone remote command, which uses the following syntax:

```
zone remote gatekeeper-name domain-name [ras-IP-address] [invia inbound-gatekeeper | outvia outbound-gatekeeper [enable-intrazone]]
```

To configure local zones, use commands like the following:

```
Router> enable
Router# configure terminal
Router(config)# gatekeeper
Router(config-gk)# zone local myGK mydom.com 10.16.193.158 invia myGK outvia
myGK enable-intrazone
Router(config-gk)# exit
```

The key command here is the zone local command, which uses the following syntax:

```
zone local gatekeeper-name domain-name [ras-IP-address] [invia inbound-gatekeeper | outvia outbound-gatekeeper [enable-intrazone]]
```

For more details on configuring gatekeepers for functionality with a Cisco UBE, read the “Configuring Cisco Unified Border Element with Gatekeeper” configuration guide available at www.cisco.com/en/US/docs/ios/voice/cubekg/configuration/guide/ve-gk-config.html.

> **Exam Watch**
> 
> Remember that you must use a via-zone to allow a gatekeeper to work with the Cisco UBE and that the zone local and zone remote commands are used to accomplish this configuration.