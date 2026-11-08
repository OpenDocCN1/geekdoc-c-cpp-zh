
unreliable channels between the endpoints. A call may be directly between two endpoints or may include other H.323 entities such as a gatekeeper or MC (Multipoint Controller). In case of interworking with some endpoints via a gateway, all the channels terminate at the gateway, where they are converted to the appropriate representation for the end system. Typically, a call is between two users for the purpose of communication, but may include signaling-only calls. An endpoint may be capable of supporting multiple simultaneous calls.

- **Endpoint** An H.323 terminal, gateway, or MCU. An endpoint can call and be called. It generates and/or terminates information streams.

- **Gatekeeper** The gatekeeper is an H.323 entity on the network that provides address translation and that controls access to the network for H.323 terminals, gateways, and MCUs. The gatekeeper may also provide other services to the terminals, gateways, and MCUs, such as bandwidth management and locating gateways.

- **H.323 entity** Any H.323 component, including terminals, gateways, gatekeepers, MCs, MPs (Multipoint Processors), and MCUs.

- **Multipoint Control Unit** The Multipoint Control Unit (MCU) is an endpoint on the network that provides the capability for three or more terminals and gateways to participate in a multipoint conference. It may also connect two terminals in a point-to-point conference, which may later develop into a multipoint conference. The MCU generally operates in the fashion of an H.231 MCU; however, an audio processor is not mandatory. The MCU consists of two parts: a mandatory Multipoint Controller (MC) and optional Multipoint Processors (MPs). In the simplest case, an MCU may consist only of an MC with no MPs. An MCU may also be brought into a conference by the gatekeeper without being explicitly called by one of the endpoints.

- **Terminal** An H.323 terminal is an endpoint on the network that provides for real-time, two-way communications with another H.323 terminal, gateway, or Multipoint Control Unit. This communication consists of control, indications, audio, moving color video pictures, and/or data between the two terminals. A terminal may provide speech only, speech and data, speech and video, or speech, data, and video.

- **Zone** A zone is the collection of all terminals, gateways, and Multipoint Control Units (MCUs) managed by a single gatekeeper. A zone has one and only one gatekeeper. A zone may be independent of network topology and may comprise multiple network segments that are connected using routers or other devices.

A few additional terms are important in the Cisco H.323 networking world. First, a *zone prefix* is a number prefix that defines the extensions available within a zone. A zone can include multiple prefixes. A zone prefix can define a specific extension or prefixes based on wildcards such as 3... or 4... to indicate any extensions from 300 to 399 or 400 to 499, respectively.

Second, technology prefixes may be used. A *technology prefix* is an optional parameter that defines a prefix to indicate a specific technology is in use and that the call should be routed to the server that understands the technology. For example, the prefix 3# may be used to indicate that a fax call is being made, and the call could be routed to the server or gateway that can process the fax.

Third, when a call is unresolved by the technology prefix, the *default technology prefix* is used. The default technology prefix is assigned in gatekeeper configuration mode using the gw-type-prefix command. For example, the following command indicates that a gateway registered to process 1# calls should be used if the gatekeeper does not recognize the number or a specific technology prefix:

```text
Router1(config-gk)# gw-type-prefix 1# default-technology
```

> **Exam Watch**
>
> Remember that zone prefixes define the extensions available within a zone. Technology prefixes are used to specify a particular technology such as a fax or modem. The default technology prefix is used if the user does not enter a technology prefix.

## CERTIFICATION OBJECTIVE 14.05

## 642-436: Implement a Gatekeeper

Implementing a gatekeeper is really a three-step process. First, you will need to set up the zones and prefixes on the gatekeeper. Second, you will need to configure the gateways to use the gatekeeper. Finally, you should verify the gatekeeper's configuration is appropriate for your needs.

### Configuring Zones

Zones can be configured as local zones or remote zones. The local zone is the zone controlled by the gatekeeper on which it is created. The remote zones are zones managed by other gatekeepers. The zone local command is used to create the local zone. The zone remote command is used to specify remote zones. The following commands provide examples of zone configuration:

```text
Router1(config)# gatekeeper
Router1(config-gk)# zone local gk1 sysedco.com
Router1(config-gk)# zone remote gk2 sysedco.com 10.1.4.1 123 cost 25 priority 35
Router1(config-gk)# no shutdown
Router1(config-gk)# exit
```

In the preceding example, the zone local command configures the zone-name parameter to gk1 and the domain-name parameter to sysedco.com. The result is a local zone named gk1.sysedco.com. The zone remote command sets the remote zone-name parameter to gk2 and the domain-name parameter to sysedco.com. The result is a remote zone named gk2.sysedco.com. Additionally, the remote zone is reachable through the IP address of 10.1.4.1 with a cost of 25 and a priority of 35. Both the cost and priority parameters may be set to any number from 1 to 100, and the default value, when not specified, is 50. When multiple remote zones are configured, the cost and priority are used to select the first remote zone to try. A lower cost and higher priority cause the zone to be used before other zones.

With the zones enabled, you must now configure the zone prefix or prefixes. You can stay in gatekeeper configuration mode, indicated by the (config-gk) CLI prompt, and configure the prefixes at the same time, or you can enter gatekeeper configuration mode again, as in the following example:

```text
Router1(config)# gatekeeper
Router1(config-gk)# zone prefix gk1 2...
Router1(config-gk)# exit
```

The preceding example indicates that the gk1 gatekeeper is responsible for all extensions from 2000 to 2999. If the zone includes multiple extensions, simply enter an additional zone prefix command for each extension or extension block by using wildcards.

Finally, you can restrict the IP subnets that should be included in the zone. This action forces IP phones on one subnet to use a particular gatekeeper, and therefore, to participate in that gatekeeper's zone. The zone subnet command is used to configure these restrictions, as in the following example:

```text
Router1(config)# gatekeeper
Router1(config-gk)# zone subnet gk1 10.1.1.0 255.255.255.0 enable
Router1(config-gk)# exit
```

In addition to accepting specific subnets, you can configure a gatekeeper to accept all subnets with the zone subnet gatekeeper_name default command.

Now that the gateway is configured to use the gatekeeper, a single dial peer must be created to indicate that the gatekeeper should be used for all four-digit extensions. The dial-peer commands in the preceding example perform this operation. Notice, specifically, the session target ras command, which indicates that a gatekeeper (which is a RAS server) should be used for all four-digit extensions.

### Verifying Gatekeeper Configuration

After the gateways have been configured to use the gatekeeper, as explained in the preceding section, the gatekeeper operations can be verified. Several show commands are useful for verification, including:

- **show gatekeeper status** — This command displays the gatekeeper state, the zone name, whether accounting is enabled or disabled, security features, and the bandwidth limits and utilization.

- **show gatekeeper calls** — This command shows all calls currently in progress that were established through the gatekeeper.

- **show gatekeeper endpoints** — Interestingly, this command shows the gateways because they are considered endpoints by the H.323 standard. It's important to remember that this command is not limited to showing IP phones.

- **show gatekeeper zone** — This command displays the zone configuration information, including prefixes and subnets.

> **Exam Watch**
>
> Be sure to know which show commands do what in relation to gatekeeper configuration and operation verification. They are very likely to show up on the CVOICE exam.
