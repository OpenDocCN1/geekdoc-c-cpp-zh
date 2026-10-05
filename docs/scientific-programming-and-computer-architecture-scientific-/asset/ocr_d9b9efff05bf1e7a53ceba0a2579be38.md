# 6.2. High-performance network architecture

Infiniband, which is an open standard, is a leading technology in high-performance networking. The technology has stabilized over the past decade or so, and almost all large and small computing clusters use Infiniband or a proprietary variation. In this section, we review three principal features of Infiniband: network topology, kernel-free messaging, and one-sided communication. These aspects of the network have an influence on the way MPI programs are written, as shown in the next section.

+   - Network topology is the graph used to connect computers. On the Internet, the graph is not regular or structured, although it is far from random (the Internet is a heavily designed network). In high-performance networks, the graphs are far more regular and structured.

Every time information is transferred over the Internet, the message passes through the operating system kernel at both the sender and the receiver. For example, when a send button is pressed on an email client, the email is first copied to kernel buffers. It is transferred to the network card at the client site before traveling to the server. The network card on the server copies the email to kernel buffers before passing it along to some server or the receiving client.

Kernel copies create considerable overhead and the Linux kernel goes to great lengths to avoid excessive copying. In Infiniband, kernel copies can be avoided altogether. Information is copied directly between the Infiniband network card and the DRAM memory owned by the client program.

Communication over the Internet is two sided, although that would be invisible to most users. When a link is followed to download a page, the web server executes send() calls (these are defined inside the operating system kernel) to transmit the page and the browser executes matching recv() calls (these too are in the kernel) to receive it.

In a one-sided network such as Infiniband, the entire transaction can be carried out by making a single call at either the sender or the receiver. There is no reason to match sending with receiving.

To be clear, one-sided communication does not mean that all the network activity is at either the sender or receiver but not both. In any communication, there will be network activity involving the Infiniband adapters at both the sender and the receiver. One-sided means that a function can initiate and complete the data transfer is made at either the sender or the receiver but not necessarily.

In section 6.2.1, we describe the fat-tree network topology. In a large network, a typical user gets control of only a small fraction of the nodes. An advantage of the