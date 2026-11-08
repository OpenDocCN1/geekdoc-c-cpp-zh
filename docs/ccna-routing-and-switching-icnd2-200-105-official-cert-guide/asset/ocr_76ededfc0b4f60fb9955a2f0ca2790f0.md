**2.** Which of the following configuration settings does not have a separate IPv4/EIGRP for IPv4 and IPv6/EIGRP for IPv6 setting, instead using one setting that both EIGRP for IPv4 and EIGRP for IPv6 use?

+   a. Interface bandwidth
+   b. Hello timer
+   c. Variance
+   d. Maximum paths

**3.** An enterprise uses a dual-stack model of deployment for IPv4 and IPv6, using EIGRP as the routing protocol for both. Router R1 has IPv4 and IPv6 addresses on its G0/0 and S0/0/0 interfaces only, with EIGRP for IPv4 and EIGRP for IPv6 enabled on both interfaces and the router ID explicitly set for both protocols. Comparing the EIGRP for IPv4 and EIGRP for IPv6 configuration, which of the following statements is true?

+   a. The EIGRP for IPv6 configuration uses the router eigrp *asn* global command.
+   b. Both protocols use the *router-id router-id* router subcommand.
+   c. Both protocols use the *network network-number* router subcommand.
+   d. The EIGRP for IPv6 configuration uses the *ipv6 eigrp asn* interface subcommand.

**4.** Three redundant IPv6 routes exist on R1 to reach IPv6 subnet 9 (2009:9:9:9::/64), a subnet connected to Router R9’s G0/0 interface. R1’s current successor route uses R2 as the next hop, with feasible successor routes through Routers R3 and R4. Then, another engineer makes changes to the configuration in the network, resulting in R1 having no routes to reach subnet 9. Which of the answers lists one configuration that would result in R1 having no routes at all to subnet 9?

+   a. Make R9’s G0/0 interface passive.
+   b. Change R2’s EIGRP ASN to some other number, but otherwise keep the same configuration.
+   c. Change the Hello timers on all of R1’s interfaces from 5 to 4.
+   d. Change R1’s EIGRP ASN to some other number, but otherwise keep the same configuration.

**5.** R1 and R2 are routers that connect to the same VLAN. Which of the answers list an item that can prevent the two routers from becoming EIGRP for IPv6 neighbors? (Choose two answers.)

+   a. Mismatched Hello timers
+   b. Mismatched ASNs
+   c. IPv6 addresses in different subnets
+   d. Using the same router ID
+   e. One passive router interface (used on this link)