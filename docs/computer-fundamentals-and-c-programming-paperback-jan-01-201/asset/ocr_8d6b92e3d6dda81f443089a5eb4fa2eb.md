**telnet** and **ftp** are two important commands used in a network and your Linux system supports both. Modern Windows systems support **ftp** from the command prompt but has the **telnet** command disabled. You can of course enable it if you want *(2.14.2)*.

# ### 2.13.2 The TCP/IP Model—The Four Layers

The TCP/IP model handles network communication using a four-layered model (Fig. 2.25). Data are divided into packets and each packet moves from one layer to another. Each layer handles a specific function of the communication process. When sending data, a layer adds information to a packet that helps in routing and reassembly. Sent data move down the following layers:

+   * *Application layer*, representing the application that generates data. New services are constantly added at this layer. The applications representing Google Chrome or Skype belong to this layer.
+   * *Transport layer* This layer splits the received data into packets, each packet containing a sequence number. The dominant protocol here is TCP (Transmission Control Protocol), which makes the transmission totally reliable. TCP will retransmit a data packet if acknowledgment of receipt is not received from the other side.
+   * *Internet layer*, which uses IP (Internet Protocol) as the protocol. IP takes care of addressing by encapsulating each packet with the source and destination addresses (the reason why they are called *IP addresses*).
+   * *Network access layer*, which finally converts the destination IP address to the MAC address of the network interface card *(1.15.1)*. ARP (Address Resolution Protocol) handles this translation.

![](bbox=[0.28, 0.68, 0.72, 0.94])