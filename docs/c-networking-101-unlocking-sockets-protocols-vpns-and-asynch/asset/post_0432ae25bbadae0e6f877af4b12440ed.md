
## Using Tracert/Traceroute

The tracert command (known as traceroute on Linux and macOS) is a command-line tool used to track and display the route that a packet takes to reach a destination on a network. It displays the series of IP addresses that the packet travels through to reach the destination. This tool is especially useful for troubleshooting network issues, as it can help to identify where along the path the problem occurs.

Below is how it works in detail:

To use tracert or traceroute, open your command line interface and type tracert (on Windows) or traceroute (on Linux or macOS), followed by the IP address or domain name of the destination host. For example, tracert www.google.com or traceroute www.google.com.

The tool will then send packets towards the destination and list each router or hop along the way. Each line represents one hop, and it displays the IP address (and often the domain name) of the router at that hop. Now, let us look at a few examples:

## Example 1: Basic Traceroute

In your terminal, type tracert www.google.com (on Windows) or traceroute www.google.com (on Linux or macOS). This will begin tracing the route that packets take from your machine to Google's server. Each line represents a hop along the route.

## Example 2: Specifying the Number of Hops

Sometimes, you might want to limit the number of hops that traceroute will attempt before giving up. To do this, you can use the `-h` option followed by the maximum number of hops. For instance:

On Linux/macOS:

```bash
traceroute -m 5 www.google.com
```

(Trace the route to Google's server, but give up after 5 hops.)

On Windows, you would use the `-h` option like this:

```bash
tracert -h 5 www.google.com
```

## Using Nslookup

The nslookup command is a network administration tool for querying the Domain Name System (DNS) to obtain domain name or IP address mappings, or any other specific DNS records. It stands for “name server lookup”. This tool can be used from a command-line interface and is available on most networked computer systems.

Below is how it works in detail:

To use nslookup, open your command-line interface and type nslookup, followed by the domain name or IP address you want to query. For example, nslookup www.google.com.

The tool will then return the domain name or IP address associated with that domain name, as well as the name server that provided the information.

Now, let us look at a few examples:

### Example 1: Basic Nslookup

## Using Netstat

The netstat command (network statistics) is a command-line tool that displays network connections (both incoming and outgoing), routing tables, and a number of network interface and network protocol statistics. It is useful for checking your network's overall health, finding out how well your firewall is working, and spotting suspicious network activity.

To use netstat, you open your command-line interface and type netstat, possibly followed by some options. By default, it shows a list of active sockets for each protocol it supports. Now, let us look at a few examples:

### Example 1: Basic Netstat

In your terminal, type netstat. This will list all current network connections, along with the protocol used, local and foreign addresses, and the state of the connection.

### Example 2: Displaying Only Listening Sockets

You can use netstat to display only sockets that are listening for incoming connections. To do this, you would type netstat -l. This is useful to quickly check what services are waiting for connections on your machine.

### Example 3: Displaying Statistics

Netstat can also display statistics for each network protocol. To do this, you would type netstat -s. This will print detailed statistics for each protocol, like the number of packets received, transmitted, discarded, etc.

### Example 4: Continuously Display Network Status

To make netstat continuously refresh network status, you can use the `-c` option, as in netstat -c. This will refresh the information every second, allowing you to monitor real-time changes to your network.

## Exploring Wireshark

## About Wireshark

Wireshark is a potent, open-source tool that enables deep inspection of network traffic, making it invaluable for network troubleshooting and protocol analysis. Its functionality encompasses various areas, such as software and communications protocol development, effectively serving as a diagnostic microscope for network health. Wireshark captures and displays data packets transmitted within a network, thereby offering a granular view of traffic details. This detailed insight makes it possible to identify anomalies, bottlenecks, and potential security threats in real time. Furthermore, it can decode and analyze data from different network protocols, providing a versatile tool for IT professionals, network administrators, and developers to optimize and secure their networks.

## Features

Wireshark has several features that make it a powerful tool for network analysis:

- Deep inspection of hundreds of protocols.
- Live capture and offline analysis.
- Ability to read/write many different capture file formats.
- Filtering and coloring rules can be applied for more effective analysis.
- Rich VoIP (Voice over IP) analysis.

## Installation of Wireshark

Begin by updating your system's package list using the following command:

```bash
sudo apt update
```

After updating the system, install Wireshark using the command:

```bash
sudo apt install wireshark
```

During the installation, a popup window will appear asking whether non-superusers should be able to capture packets. Choose “Yes” if you want to allow this.

After the installation process completes, you can verify it by typing:

```bash
wireshark --version
```

This will display the version of Wireshark that you installed.

## Wireshark Configuration

Start Wireshark from the terminal by just typing wireshark and pressing Enter. Alternatively, it should also appear in your system's application menu.

When Wireshark opens, you will see a list of the network interfaces on your system. Click the name of the interface that you want to capture data from. This will start the capture process.

You can filter the traffic using the “Apply a display filter” field. For example, typing http will only display HTTP traffic.

Click the Stop button to stop capturing traffic. Now you can analyze the traffic in detail.

## Exploring Tcpdump

## About Tcpdump

Tcpdump is a versatile command-line packet analyzer tool prevalent in Unix and Linux distributions. Essentially, it's a network monitoring tool that allows users to capture or “sniff” TCP/IP packets and other types of data packets in real time, flowing in and out of network interfaces. By capturing these packets, users can diagnose network issues, analyze network performance, or scrutinize the data traffic on a network. Its command-line interface ensures a lightweight footprint, making it an efficient and powerful tool for network analysis and troubleshooting, whether it's for understanding network protocols, crafting security policies, or investigating network anomalies.

## Features

- **Versatile:** tcpdump can capture or “sniff” traffic on any network to which the computer is attached.
- **Expressive:** Its filtering capability allows users to zero in on traffic based on specific criteria.

This command reads packets from filename.pcap.

Capture ICMP packets using a filter:

```bash
sudo tcpdump icmp
```

## Summary

In this chapter, we deeply delved into the vital area of network troubleshooting. We started by understanding the network troubleshooting methodology, a systematic approach often used by network administrators to identify, diagnose, propose solutions, test, and document network problems. This methodology is crucial to avoid recurrent issues and maintain a reliable network infrastructure.

Next, we explored essential network troubleshooting tools, beginning with “ping”, a simple yet effective tool used to verify network host reachability and network latency. We then covered “tracert” (traceroute), a powerful command-line tool used to track the path that a packet takes from the source system to the destination system. Moving on, we discussed “nslookup”, a command-line tool used for querying the DNS (Domain Name System) to obtain domain name or IP address mappings, and other DNS records. We also went through “netstat”, a versatile tool that provides information and statistics about protocols in use and current TCP/IP network connections.
