# Exercise 17.49

Install one or all of the earlier IDS packages on your Linux system, using the package management system available. How do you deploy fail2ban, and how do you control its environment? For example, how do you “unblock” an IP address using fail2ban? Test this on your Linux system.

# Exercise 17.50

What are the capabilities and uses of Wireshark? Give a description of it in terms of the IDSs we described earlier, and then install Wireshark and use it on your Linux system.

# 17.9.4 Linux Security Software

All larger Linux computer server systems, as well as individual desktop systems used by an ordinary user, can have several types of network-based and host-based security software available to detect malicious activity, protect systems and data, and support intrusion detection and the appropriate responses to them. They can be organized into the following categories:

+   - IDS and IPS
+   - Remote Access Software
+   - Web Proxies
+   - Vulnerability Management Software
+   - Authentication Servers
+   - Routers
+   - Firewalls
+   - Network Quarantine Servers

We covered some of the details of Intrusion Detection and also give a more complete description of Firewalls in the next section.

# 17.9.4.1 System Firewall

A firewall is a facility that prevents unauthorized access to or from a private network or a computer. Firewalls can be implemented in either hardware, software, or a combination of both. Firewalls are primarily used to prevent unauthorized access to a private network or intranet, from the Internet. All traffic entering or leaving a single computer or intranet passes through the firewall, which examines each message and blocks those that do not meet the specified security criteria or firewall rules.

In addition to limiting access to your computer and network, a firewall is also useful for allowing remote access to a private network through secure authentication certificates and logins. A common practice is to let a stand-alone computer serve as a single hardware firewall to a private network.

Hardware firewalls can be purchased as a stand-alone product. They can also be found integral to broadband routers, such as the Actiontec PK5000. Most hardware firewalls will have a minimum of four network ports to connect other computers, but for larger networks, business networking firewall solutions are available.

In Linux, if the firewall is active (enabled, or running), all incoming traffic is usually blocked until you specify a TCP or UDP port that traffic is allowed to come in on. Also, usually all outgoing traffic on all ports is allowed. In the following sections, we describe the Uncomplicated FireWall (ufw) for the Debian-family of Linux (including Debian, Ubuntu, and Linux Mint), and also firewalld for CentOS.

To determine whether the firewall is active, use the following systemd command on any of our representative Linux systems:

```
$ systemctl status firewall_name
```

where firewall_name is ufw on the Debian-family and firewalld on CentOS.