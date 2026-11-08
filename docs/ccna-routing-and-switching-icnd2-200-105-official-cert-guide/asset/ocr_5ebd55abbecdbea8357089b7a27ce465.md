> > **NOTE** If the routers also configured the IPsec encryption part of the tunnel, just after the steps shown in Figure 15-14, the receiving router would then decrypt the original packet.

# ## Configuring GRE Tunnels

Configuring GRE tunnels requires only a few commands. The challenge with GRE configuration comes in organizing the configuration parameters. The configuration requires a tunnel interface, with IP addresses from the secure part of the network configured with the `ip address` interface command. It also requires that the two routers declare both their own IP address (source) and the other router's IP address (destination), used in the unsecure part of the network. Figure 15-15 shows the organization of the various configuration parameters.

![](bbox=[0.16, 0.32, 0.651, 0.548])

**Figure 15-15** *GRE Tunnel Configuration: Relationship of Parameters*

The following list details the configuration steps on each router:

+   1. **Step 1.** Use the `interface tunnel number` global command to create a tunnel interface. The interface numbers have local meaning only and do not have to match between the two routers.
+   2. **Step 2.** (Optional) Use the `tunnel mode gre ip` interface subcommand in tunnel interface mode to tell IOS to use GRE encapsulation on the tunnel. (This is the default setting for a tunnel interface.)
+   3. **Step 3.** Use the `ip address address mask` interface subcommand to assign an IP address to the tunnel interface, using a subnet from the secure network's address range. The two routers on the tunnel should use addresses from the same subnet.
+   4. **Step 4.** Configure the tunnel's source IP address in the unsecure part of the network in one of two ways. Regardless of the method, the local router's source IP address must match the other router's tunnel destination.
+       - **Step 4A.** Use the `tunnel source ip-address` tunnel interface subcommand to directly set the tunnel's source IP address.
+       - **Step 4B.** Use the `tunnel source interface-id` tunnel interface subcommand to indirectly set the tunnel's source IP address by referencing an interface on the local router.