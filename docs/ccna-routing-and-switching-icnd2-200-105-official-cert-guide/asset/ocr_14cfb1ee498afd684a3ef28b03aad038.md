5. An enterprise uses Cisco IOS routers and DSL connections to local ISPs for their retail locations. The ISPs require the use of PPPoE. The routers at each retail site use dynamically learned public IP addresses as learned from the ISPs. Each router uses its F0/0 interface to connect to an external DSL modem, which then connects to a phone line. Which of the following is the most likely choice for configuring the router to use the IP address as assigned by the ISP?

+   - a. Interface F0/0 has an ip address dhcp interface subcommand.
+   - b. Some dialer interface has an ip address dhcp interface subcommand.
+   - c. Some dialer interface has an ip address negotiated interface subcommand.
+   - d. Interface F0/0 has an ip address negotiated interface subcommand.

6. An enterprise uses Cisco IOS routers and DSL connections to local ISPs for their retail locations. The ISPs require the use of PPPoE. The following output listed comes from one such router (R1). Which of the following answers are true about the configuration on Router R1 and its current PPPoE state? (Choose two answers.)

```
```
R1# show pppoe session
      1 client session

Uniq ID  PPPoE  RemMAC          Port                    VT  VA         State
         SID    LocMAC                                      VA-st      Type
    N/A  1      0200.0000.3333  Gi0/0                   Di1 Vi1      UP
               0200.0000.3003                              UP
```
```

+   - a. The configuration includes PPPoE commands under interface virtual-access 1.
+   - b. Dialer interface 1 and virtual-access 1 are bound together.
+   - c. Interface G0/0 is using MAC address 0200.0000.3333.
+   - d. The PPPoE session is currently working.

7. An enterprise uses Cisco IOS routers and DSL connections to local ISPs for their retail locations. The ISPs require the use of PPPoE. A network engineer connects to the console of one router at a retail office, issues the show pppoe session command, and the router just returns a command prompt, with no lines of output. If you knew the problem was related to the configuration on the local router, which one of the four following areas would be the best area to recommend for your colleagues to investigate in their next troubleshooting step?

+   - a. Look at the commands on the physical Ethernet interface
+   - b. Look at the dialer interface commands specific to PPP
+   - c. Look at the commands specific to IPv4 address learning
+   - d. Look at the commands in the running-config file for the virtual-access interface