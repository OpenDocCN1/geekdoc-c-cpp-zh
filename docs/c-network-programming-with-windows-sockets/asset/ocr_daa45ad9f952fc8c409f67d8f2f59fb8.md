# ## Routing

Routing is the method by which packets of data are sent from one computer to another in the most efficient way possible. The routing process is composed of several components as follows:

+   - Determining what paths are available between the source and destination computers
+   - Selecting the “best” path between the source and destination computers where “best” may mean different things depending on the goals
+   - Using those paths to reach other computers
+   - Adjusting the datagram formats to fit into the underlying physical network technology

In a TCP/IP network, routing is performed by the IP layer. The network id of the destination computer’s IP address as well as the subnet mask are used by the IP layer to make routing decisions.

# ## Default Gateway

In an interconnected computer network, or internet, some method is required to deliver data to computers that reside on another connected network. By specifying a default gateway, the IP layer of the sending computer “knows” to what destination it should forward data that has a destination which isn’t on the local network. See Figure 2.10 for a simple network arrangement. When 166.78.4.139 sends data to 166.78.4.10, the IP layer takes the subnet mask, which in this case 255.255.255.0, and performs a logical AND operation on both the source and destination IP addresses. The result in this case is 166.78.4.0 for both addresses, which tells the IP layer that both computers are on the same subnet. The data is sent directly to 166.78.4.10. When 166.78.4.139 sends data to 166.78.1.5, the IP layer again uses the subnet mask, and the results are 166.78.4.0 for the source and 166.78.1.0 for the destination. These numbers don’t match, which signals the IP layer that the computers reside on different subnets. The sending computer can’t send directly to 166.78.1.5. The data must be sent to the default gateway, which is a computer that has two IP addresses and resides on two distinct subnets. The data is first sent to 166.78.4.2 and then forwarded on to 166.78.1.5.