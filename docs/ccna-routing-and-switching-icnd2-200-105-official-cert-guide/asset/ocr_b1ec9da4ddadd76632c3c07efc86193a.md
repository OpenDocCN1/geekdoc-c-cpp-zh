IOS knows that it is illegal to overlap the ranges of addresses implied by a subnet. In this case, because both subnets would be connected subnets, this single router knows that these two subnets should not coexist because that would break subnetting rules, so IOS rejects the second command.

As an aside of how IOS handles these errors, IOS only performs the subnet overlap check for interfaces that are not in a shutdown state. When configuring an interface in shutdown state, IOS actually accepts the `ip address` command that would cause the overlap. Later, when the `no shutdown` command is issued, IOS checks for the subnet overlap and issues the same error message shown in Example 21-6. IOS leaves the interface in the shutdown state until the overlap condition has been resolved.

IOS cannot detect the configuration of overlapping subnets on different routers, as shown in Example 21-7. The example shows the configuration of the two overlapping subnets on R2 and R3 from Figure 21-13.

**Example 21-7** *Two Routers Accept Overlapped Subnets*

```
~~~
! First, on router R2
R2# configure terminal
R2(config)# interface G0/0
R2(config-if)# ip address 172.16.4.1 255.255.254.0
! Next, on router R3
R3# configure terminal
R3(config)# interface G0/0
R3(config-if)# ip address 172.16.5.1 255.255.255.0
~~~
```

# ## Pointers to Related Troubleshooting Topics

A router's data plane may fail due to features beyond those mentioned in this chapter or in this book. However, other chapters of the ICND1 and ICND2 books explain troubleshooting of a couple of other features that directly impact a router's forwarding logic. This short section references those other topics for completeness, even though the details sit in other chapters.

# ## Router WAN Interface Status

One of the steps in the IP routing troubleshooting process described earlier, in the “Router LAN Interface and LAN Issues” section, says to check the interface status, ensuring that the required interface is working. For a router interface to be working, the two interface status codes must both be listed as up, with engineers usually saying the interface is “up and up.”

To fully troubleshoot the IPv4 data plane over WAN links, you should look closely at the troubleshooting topics in Chapter 13, “Implementing Point-to-Point WANs,” of this book. Anything that prevents a serial link from being in an up/up state would of course prevent the routers on that link from sending packets to each other.

In addition, note that a link can be in an up/up state on both ends but still have IPv4 forwarding issues. A serial link with both interfaces up/up means that Layers 1 and 2 work well, but Layer 3 might still have an issue. In particular, the classic case is the misconfiguration of IPv4 addresses on the two ends of the link, such that the addresses are in different subnets.

Make sure to review all these details about troubleshooting WAN links in Chapter 13.