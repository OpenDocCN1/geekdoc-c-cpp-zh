Examples of Transport layer protocols and functions include TCP and UDP. The Transmission Control Protocol (TCP) is the primary protocol used for the transmission of connection-oriented data in the TCP/IP suite. HTTP, SMTP, FTP, and other important Layer 7 protocols depend on TCP for reliable delivery and receipt of data. The User Datagram Protocol (UDP) is used for connectionless data communications. For example, when speed of communications is more important than reliability, UDP is frequently used. Because voice data either has to arrive or not arrive (as opposed to arriving late), UDP is frequently used for the transfer of voice and video data.

TCP and UDP are examples of transport-entities at Layer 4. These transport-entities will be served by the Network layer. At the Transport layer, the data is broken into segments if necessary. If the data will fit in one segment, then the data becomes a single segment. Otherwise, the data is segmented into multiple segments for transmission.

The Transport layer takes the information about your e-mail message from the Session layer and begins dividing (segmenting) it into manageable chunks (packets) for transmission by the lower layers. Figure 2-5 shows the e-mail after the processing at the Transport layer.

on the job

> *You've probably heard of TCP and UDP ports. For example, port 80 is used for HTTP with the TCP protocol, port 21 is used for Telnet, and so on. The ports are used to indicate the application (at the upper layers) that should process the incoming data. Applications listen on these assigned ports.*

# ### Network Layer

The Network layer is defined as providing “the functional and procedural means for connectionless-mode (UDP) or connection-mode (TCP) transmission among transport-entities and, therefore, provides to the transport-entities independence of routing and relay considerations.” In other words, the Network layer says to the Transport layer, “You just give me the segments you want to be transferred and tell me where you want them to go. I’ll take care of the rest.” This segregation of communication is why routers do not have to expand data beyond Layer 3 to route the data properly. For example, an IP router does not care if it’s routing an e-mail message or voice conversation. It only needs to know the IP address for which the packet is destined and any relevant QoS parameters in order to move the packet along.

Examples of Network layer protocols and functions include IP, ICMP, and IPSec (Internet Protocol Security). The Internet Protocol (IP) is used for addressing and routing of data packets to allow them to reach their destination. That destination