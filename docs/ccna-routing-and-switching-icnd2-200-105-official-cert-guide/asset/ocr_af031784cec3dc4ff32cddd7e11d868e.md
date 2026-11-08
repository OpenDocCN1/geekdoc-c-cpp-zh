Implementing MLPPP requires a longer configuration than most features discussed in this book. So first, to set the context a bit, think about these main three configuration requirements for MLPPP:

+   1. **Step 1.** Configure matching multilink interfaces on the two routers, configuring the interface subcommands for all Layer 3 features (IPv4, IPv6, and routing protocol) under the multilink interfaces (and not on the serial interfaces).
+   2. **Step 2.** Configure the serial interfaces with all Layer 1 and 2 commands, like clock rate (Layer 1) and PPP authentication (Layer 2).
+   3. **Step 3.** Configure some PPP commands on both the multilink and serial interfaces, to both enable MLPPP and associate the multilink interface with the serial interfaces.