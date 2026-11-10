# 1.14 COMPUTERS IN A NETWORK

Most organizations, large or small, no longer have standalone computers. Today, computers cooperate with one another by being connected to a network. An authorized user can now share their files with other users. An application run by multiple users can now be hosted on a single machine instead of being stored on individual machines. Many network applications today are designed in a way that enable sharing of the workload by multiple machines. As rightly perceived by Sun Microsystems many years ago, “the network is the computer.”

Apart from sharing files and programs, a network allows the sharing of scarce hardware resources by all connected computers. A printer can be used by several users if the printer itself is connected to one of the computers in the network. The computer (or *node*, in network parlance) that offers these services would need to be more powerful than the computers it serves. That’s how *servers* came into being as the central nodes in a network. Servers also form the backbone of the largest network of all—the Internet.

All networked nodes need a common addressing scheme that would ensure delivery of data to the right node. The scheme used by most is *Ethernet*, a hardware standard that defines the addressing, cabling and signaling requirements of the network. Ethernet is currently the dominant technology, having replaced the *token ring* and *FDDI* technologies. In this scheme, data are divided into *frames* containing the source and destination addresses. A set of network *protocols* (rules) are also used for data transmission, but they will be discussed in Chapter 2.

> Note: Ethernet, token ring and FDDI are hardware technologies. For a network to function, a set of network (software) protocols also need to run. *TCP/IP* is the most dominant network protocol and it powers the Internet.

# 1.14.1 Network Topology

There are a number of ways or *topologies* of connecting computers (Fig. 1.7), each having its own merits and demerits. The *bus topology* uses a single cable as a bus to which all computers are connected. The failure of a single node doesn’t disrupt the communication between the remaining nodes.

The *star topology* uses a central hub to which all nodes are connected. Because network traffic passes through the hub, the entire network fails if the hub fails to work. On the other hand, new nodes can be added without disrupting the service.

Nodes using the *ring topology* are connected in a closed loop without using a hub. Data moves from one node to the next one which examines each packet to determine whether it should be allowed to move further on to the next node. For uni-directional rings, failure of one node causes the network to shut down.

Nodes in a *mesh topology* are connected to one another, offering a choice of multiple routes for data to travel. When a node breaks down, the packet simply changes its route. This is the most expensive of all the topologies, and is found mainly in corporate networks.