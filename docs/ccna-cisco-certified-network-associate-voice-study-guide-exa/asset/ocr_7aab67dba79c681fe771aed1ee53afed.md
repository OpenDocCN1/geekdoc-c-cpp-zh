These private IP addresses fall into three different ranges that were originally set aside according to the A, B, and C classes. These address ranges are:

+   - 10.x.x.x
+   - 172.16.x.x–172.31.x.x
+   - 192.168.x.x

The class A private address space ranges from 10.0.0.1 to 10.255.255.254, provides about 16.7 million IP addresses, and can be divided into thousands of networks using classless subnetting. The class B private address space ranges from 172.16.0.0 to 172.31.255.254, provides about 1 million IP addresses, and can be divided into hundreds of networks. Finally, the class C private address space ranges from 192.168.0.1 to 192.168.0.254, provides 65,556 addresses, and can be divided into hundreds of networks as well.

You'll notice that the class B private address range is the only one that provides more than one starting set of decimal values. For example, all of the class A private addresses start with 10, and all of the class C private addresses start with 192.168. The class B private address range can start with any numbers from 172.16 to 172.31.

Ultimately, there's a big difference between a globally assigned IP address and a private IP address. Globally assigned addresses are assigned by the IANA or one of the agencies serving the IANA. Private addresses can be assigned by an organization in any way they desire as long as they have implemented a network infrastructure that can support them. The benefit of private addresses is that they are set aside by the IANA and are guaranteed to never be the destination of an actual “on-the-Internet” host. This means that you'll be able to use the same IP addresses on your network as those being used on mine, and we'll still be able to communicate with each other across the Internet as long as we both implement a NAT solution, and possibly port forwarding, depending on the scenario.

As you can imagine, a private network that uses the “ten space” (a phrase for referencing the private IP addresses that are in the 10.x.x.x range) can be rather large. To reduce network traffic on single segments, we can subnet our network and increase performance. To do this, you will need to implement the appropriate subnetting scheme with subnet masks.

A subnet mask is a binary-level concept that is used to divide the IP address into a network identifier (ID) and a host ID. The network ID identifies the network on which the host resides, and the host ID identifies the unique device within that network. The two basic kinds of subnetting are classfull and classless.

Classfull (also written “classful”) subnetting simply acknowledges the class of the IP address and uses a subnet mask that matches that class. For example, a class-A IP address would use the first 8 bits for the network ID, and therefore the subnet mask would be: