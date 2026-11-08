In conclusion, for this example, if a routing problem prevents the traceroute command from working, the problem exists in one of two places: the forward route to 5.5.5.5 on Router R3, or the reverse route to 1.1.1.1 on R4.

# Telnet and SSH

The ping and traceroute commands do give networkers two great tools to begin isolating the cause of an IP routing problem. However, these two commands tell us nothing about the operation state inside the various network devices. Once you begin to get an idea of the kinds of problems and the possible locations of the problems using ping and traceroute, the next step is to look at the status of various router and switch features. One way to do that is to use Telnet or Secure Shell (SSH) to log in to the devices.

# Common Reasons to Use the IOS Telnet and SSH Client

Normally, a network engineer would log in to the remote device using a Telnet or SSH client on their PC, tablet, or any other user device. In fact, often times, the same software package does both Telnet and SSH. However, in some cases, you may want to take advantage of the Telnet and SSH client built in to IOS on the routers and switches, to Telnet/SSH from one Cisco device to the next.

To understand why, consider the example shown in Figure J-17. The figure shows arrowed lines to three separate IP addresses on three separate Cisco routers. PC1 has attempted to Telnet to each address from a different tab in PC1’s Telnet/SSH client. However, R2 happens to have an error in its routing protocol configuration, so R1, R2, and R3 fail to learn any routes from each other. As a result, PC1’s Telnet attempt to both 10.1.2.2 (R2) and 10.1.3.2 (R3) fails.

![](bbox=[0.155, 0.542, 0.775, 0.648])

**Figure J-17** *Telnet Works from PC1 to R1 but Not to R2 or R3*

In some cases, like this one, a Telnet or SSH login from the network engineer’s device can fail, while you could still find a way to log in using the telnet and ssh commands to use the Telnet and SSH clients on the routers or switches. With this particular scenario, all the individual data links work; the problem is with the routing protocol exchanging routes. PC1 can ping R1’s 10.1.1.1 IP address, R1 can ping R2’s 10.1.2.2 address, and R2 can ping R3’s 10.1.3.3 address. Because each link works, and each router can send and receive packets with its neighbor on the shared data link, you could Telnet/SSH to each successive device.

Figure J-18 shows the idea. On the left, PC1 begins with either a Telnet/SSH or a console connection from PC1 to Router R1, as shown on the left. Then the user issues the telnet 10.1.2.2 command from R1 to Telnet to R2. Once logged into R2, the user can issue commands on R2. Then from R2, the user could issue the telnet 10.1.3.3 command to Telnet to R3, from which the user could issue commands on R3.