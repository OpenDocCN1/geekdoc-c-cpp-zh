
## PING

PING stands for Packet Internet Groper and is a command used to test IP connectivity. It is useful when you are unsure if your network connection is even operating at the Network layer. The PING command varies slightly from one operating system to another, but most operating systems that support TCP/IP also support the PING command. Even Windows for Workgroups 3.11 (many years ago) included a PING command when you installed the TCP/IP protocol. The following exercise will walk you through using PING on a Windows machine.

### Exercise 17-1: Using the PING Command

In this exercise, you will use the PING command to verify that a remote system is functioning on the network. You will also use the command to perform a continuous PING to test for intermittent problems. Finally, you’ll see how you can increase and decrease the size of the PING request.

**Verify a Remote System Is Functioning**

- 1. Open a Command Prompt window.
  - a. Click Start | All Programs | Accessories and select Command Prompt.
- 2. Type `PING remote_system_IP`.
  - a. For example, if you are testing the remote system at 10.10.10.100, you would type `PING 10.10.10.100`.

**Perform a Continuous PING**

- 1. Open a Command Prompt window.
- 2. Type `PING -t localhost` and press ENTER.

You will notice that the PING command requests a response from the local machine periodically and without ceasing. If you want to test for intermittent network problems, use the `PING -t` command against a remote machine. You can stop the perpetual PING by pressing CTRL-C.

**Increase or Decrease the Size of the PING Request**

- 1. Open a Command Prompt window.
- 2. Type `PING -l 10240 localhost` and press ENTER.

The default PING request size is 32 bytes. The `-l` switch allows you to increase or decrease this size. Using the `-l` switch with the `-t` switch can be very useful when troubleshooting latency or dropped packet problems.

## TraceRt

The TraceRt (trace route) command provides you with a simple method for testing the intermediate devices between two endpoints. For example, if you are working at a computer with the IP address of 10.10.10.200 and you want to test the route to 10.10.50.200, you would type the following command:

```
TRACERT 10.10.50.200
```

The TraceRt command also provides several switches for manipulating the command. Table 17-5 outlines these switches.

Remember that operating systems implement similar tools in different ways. For example, macOS has a TraceRoute command as opposed to the Windows TraceRt command.

**Table 17-5 — TraceRt Switches**

| Switch | Description |
|---|---|
| `-d` | Does not resolve addresses to host names. This switch can speed up the TraceRt processing. |
| `-h maximum_hops` | Specifies the maximum number of hops to trace. |
| `-j host` | Forces TraceRt to route through a given host. |
| `-w timeout` | Specifies the timeout value, in milliseconds, for each reply. |
| `-R` | Traces the round-trip path for IPv6 connections. |
| `-S source_address` | Specifies the source address to use for IPv6. |
| `-4` | Forces the use of IPv4. |
| `-6` | Forces the use of IPv6. |

## PathPING

PathPING is a newer command-line tool for Windows systems that allows you to PING the devices along the path to a destination. Unlike TraceRt, PathPING also reveals the number of sent packets compared to the number of dropped or lost packets. For this reason, PathPING is an excellent tool for troubleshooting dropped packets in voice networks. The command uses the switches listed in Table 17-6.

**Table 17-6 — PathPING Switches**

| Switch | Description |
|---|---|
| `-g host` | Same functionality as the `-j` switch in TraceRt |
| `-h maximum_hops` | Specifies the maximum number of hops across which the connection should be traced |
| `-i address` | Tells PathPING to use the specified source IPv6 address |
| `-n` | Same functionality as `-d` in TraceRt |
| `-q number_of_queries_per_hop` | Specifies the number of PINGs to execute against each device in the path |
| `-w timeout` | Specifies how long to wait, in milliseconds, for each query reply |
| `-4` | Forces the use of IPv4 |
| `-6` | Forces the use of IPv6 |

## ARP

The Address Resolution Protocol (ARP) is used to resolve IP addresses to MAC addresses for LAN packet delivery. Directly linked Ethernet devices communicate with each other based on their MAC addresses; however, routers receive packets destined for IP addresses. Some mechanism must be used to resolve these IP addresses to MAC addresses, and this is where the ARP cache is utilized.

When a machine needs to resolve an IP address to a MAC address, it will first look in the ARP cache. The ARP cache contains a listing of previously resolved IP-to-MAC mappings. To see the ARP cache on Windows:

- 1. Open a Command Prompt window.
- 2. Type `ARP -a` and press ENTER.

Figure 17-3 shows sample output from the ARP command on a Windows Vista client. You can see the MAC addresses of the local network interfaces as well as the devices to which the machine has connected. For more detailed information, type `ARP -a -v`, which will provide you with a verbose listing of the ARP cache. To clear the ARP cache, simply type `ARP -d *` and all entries will be deleted.

![](img/ee67e6cd30f16bc39d653f87870eabb5_499_0.png)

## NSLookup

If you are finding it impossible to connect to devices based on their DNS or host names, you can use the NSLookup tool to query the DNS server. This tool can perform both forward and reverse lookups as well as special operations for service records. For example, to resolve the IP address of a website, type `NSLOOKUP website_domain_name`. The result will be the IP address of the website and the name of the DNS server that resolved the host name to the IP address. You can also use NSLookup in interactive mode by typing NSLOOKUP and pressing ENTER. Figure 17-4 shows the NSLookup tool working in interactive mode.

![](img/ee67e6cd30f16bc39d653f87870eabb5_499_1.png)

## Hostname

Hostname is a simple command-line tool that reveals the local machine name. Typing `hostname` at the command prompt will return the host name of the computer. You can get the same information by typing `ECHO %computername%`. The latter method has been available for many years in Windows systems, and the former method is more recent.

## NetStat

NetStat is a command-line tool that reveals network interface statistics. You can view both statistics related to communications and the currently open connections with this tool. Figure 17-5 shows the command-line options available for NetStat.

![](img/ee67e6cd30f16bc39d653f87870eabb5_500_0.png)

One of the useful features of the NetStat command is the ability to view statistics for a specific protocol. For example, you can view only TCP statistics, only IP statistics, and only UDP statistics. The `NetStat -s -p TCP` command, for example, will display only statistics for TCP communications. Figure 17-6 shows the output for viewing TCP, IP, and UDP statistics, respectively.

## CERTIFICATION OBJECTIVE 17.0.1

### 640-460: Explain Basic Troubleshooting Methods for Cisco Unified Communications Manager Express

As with most anything you troubleshoot, the first step that you should take with a Cisco Unified CME configuration is to verify proper settings. If the settings are incorrect, the device will not perform as needed. In this section, you will learn about several commands that can be used to verify CME configuration settings.

### Verifying CME Settings

One of the most important commands on a Cisco router that is used to run Cisco Unified CME is the `show running-config` command. In addition to this command, several troubleshooting show commands may be helpful. Table 17-7 provides a reference for these commands.

**Table 17-7 — CME IOS Troubleshooting Commands**

| Command | Purpose | Example |
|---|---|---|
| `debug ip` | To analyze DHCP communications | `debug ip dhcp server events` |
| `debug tftp events` | To analyze TFTP events such as Cisco IP phone firmware downloads | `debug tftp events` |
| `show telephony-service` | To view the CME settings and information | `show telephony-service tftp-bindings` |
| `debug ephone` | To verify that the ephone registration process is working | `debug ephone register` |
| `show ephone` | To determine the state of an ephone (registered, unregistered, or deceased) | `show ephone attempted-registrations` |
