fat-tree is that the bandwidth realized is relatively independent of how MPI processes are mapped to nodes of the fat-tree. The fat-tree topology is common among high-performance networks, although actual networks are approximations and not perfect realizations of the fat-tree.

In section 6.2.2, we turn to a deeper study of the Infiniband network. The discussion of MPI in the next section is informed by many architectural issues that arise in this study.

Like all modern networks, Infiniband is packetized. Data is broken up into packets before it travels over the network. Each packet has an envelope in addition to the data, and the layout of the envelope together with the data constitutes the data format. Every packet needs an envelope for the same reason that every parcel mailed needs an envelope carrying the addresses of the sender and the receiver. The parcel would be undeliverable otherwise.

Packetization and the consequent change in data format means that copying to buffers is inevitable. In Infiniband transmission, the buffers exist on the Infiniband network card (the-called host channel adapter), and packetization does not require kernel intervention. Error correction, flow control, and congestion control are also handled by the network card.

Read Direct Memory Access (RDMA) is the distinctive feature of Infiniband. RDMA allows either the sender or the receiver to make a single function call to transmit data. The function call is made from a user program. The kernel does not participate in any way in executing that call. Data transfer is entirely the responsibility of the Infiniband adapters and network.

Section 6.2.2 includes two applications to actual programming, with many to follow in the next section. The first application is a discussion of the latency of Infiniband networks. The second application is an explanation of what makes the program unsafe() of the previous section deadlock for long messages but not for short messages.

# 6.2.1 Fat-tree network

In many high-performance clusters, nodes are networked using fat-trees.4 A defining property of fat-trees, shown in figure 6.1, is that the number of links between levels is

> 4Fat-trees were discovered and made popular by Leelson (1985).