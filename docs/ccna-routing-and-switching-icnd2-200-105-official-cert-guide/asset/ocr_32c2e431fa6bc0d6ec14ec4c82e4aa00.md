# Stateless Address Autoconfiguration

IPv6’s stateless address autoconfiguration (SLAAC) provides an alternative method for dynamic IPv6 address assignment—without needing a stateful server. In other words, SLAAC does not require a server to lease the IPv6 address and record (keep state information) about which host has which IPv6 address, as is the case with the stateful DHCPv6 service.

SLAAC defines an overall process that also uses NDP and DHCPv6 with a stateless service; the server keeps no state information. First, the process takes advantage of NDP, through which the host can learn the following from any router on the link: the IPv6 prefix (subnet ID), the prefix length (mask equivalent), and the default router IPv6 address. The host uses SLAAC rules to build the rest of its address. Finally, the host uses stateless DHCPv6 to learn the DNS server IPv6 addresses. Figure 22-7 summarizes these details for easy study and reference.

![](bbox=[0.089, 0.356, 0.611, 0.508])

**Figure 22-7**  *Sources of Specific IPv6 Settings When Using SLAAC*

With SLAAC, a host learns values for three settings (prefix length, router address, and DNS servers), but the host builds the value to use as its address. To build the address, a host uses these steps:

+   1. Learn the IPv6 prefix used on the link, from any router, using NDP Router Solicitation (RS) and Router Advertisement (RA) messages.
+   2. Choose an interface ID value to follow the just-learned IPv6 prefix, either randomly or by choosing a number, or by using the host’s MAC address and using EUI-64 rules.

If the host uses the EUI-64 option, the address built by the host can be predicted. The prefix part of the address is the prefix as defined on the local IPv6 router. Then, the host’s MAC address feeds into a few EUI-64 (also called modified EUI-64) rules to change the 48-bit MAC address into a 64-bit interface ID, as follows:

+   1. Split the 6-byte (12 hex digits) MAC address in two halves (6 hex digits each).
+   2. Insert FFFE in between the two, making the interface ID now have a total of 16 hex digits (64 bits).
+   3. Invert the seventh bit of the first byte.

Figure 22-8 shows the major pieces of how the address is formed.