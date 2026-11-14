

The software component includes a special collection of routines called drivers, which are used to manage communication with individual devices or classes of devices.

The management of remote processes and information exchanges in the expanded model is complicated by intra-and intersystem delays, as well as by failures of the transport mechanism or of the remote devices themselves. The earlier model identified shared variables and messages as the principal means for executing the exchange. We now expand the scope of these concepts to include locations in remote address spaces.

The source or destination of a shared variable pair may now include an external device such as a register or set of registers in a peripheral device to which one must write initialization or configuration values, or perhaps data buffer on such a device. The message model will expand to include the invocation of methods or procedures on a remote external device.

## 15.4.4 Transport

#### transport mechanism

The transport mechanism, the physical means by which the information is moved, can be implemented by any of a great variety of physical mediums and configurations. Included among the many choices are a simple piece of wire, a bundle of fiber-optic filaments, or the surrounding air. The target of the exchange can be local – within the same array – or it can be remote – across the office, the factory, the country, or the world.

The most common and most familiar means of transport today is the familiar copper connection, although this preference is rapidly changing to fiber, air, or wireless. In the most basic case, the transport medium is simply the necessary number of wires bundled together, carrying electrical signals from one place to another. Today, however, I/O speeds are beginning to track the increasing capabilities of the processing units. As the speed increases, so must the quality of the communication channel.

We may use a number of design approaches to enable us to begin to ensure the necessary increase in quality and reliability. Two of the main causes of electrical contamination are crosstalk between adjacent conducting paths and noise induced from external sources. Crosstalk can be addressed by alternating signal and ground conductors in the conducting path or by twisting ground and signal conductors together. External contamination can be attacked by using differential signals, shielding the entire cable or the individual twisted pairs, or both.

Fiber optics provides an increased level of robustness. Prior to transport, the information is converted into optical signals that move, without electrical interference, along thin, optically conductive channels. At the end of the day, the objective remains the same: to reliably move data and control information from one place to another. At the time of this writing, fiber is a somewhat more expensive alternative to standard copper wire for most applications. In addition to the cost of the material, the difficulty of making a connection with low-cost tools remains. The strength of fiber optics is its immunity to most of the electrical contamination that affects traditional wire. Both objections will change with time and continued advances in technology.

Wireless, in the form of radio waves, offers another alternative to copper. A wireless communication network is easy to install and works very well in areas where wire infrastructure is not in place or where a temporary connection is needed. It is cheaper and more flexible than a wire-based approach. However, it is typically slower than wire and more prone to errors from environmental interference.

The organization of the medium can range from a few signal lines with information flowing in serial to a larger number of signals simultaneously transporting greater amounts of the information. No matter which transport scheme is used, a solid understanding of all timing relationships, the strengths and limitations of the medium, and the transport protocol is required.

## 15.5 EXPLORING THE MODEL

With that overview, we will now study each component of the model in greater detail. The exchange can be characterized, analyzed, and designed from a number of different perspectives. As we explore, we will begin at a high level and work down to specific details. Earlier studies of interprocess communication and synchronization have provided a solid foundation upon which we can build. The transport mechanism introduces a new consideration into the designs. As a result, we will develop the extended model starting from this point. We will begin with the vocabulary and basic concepts; these will be examined in depth as the chapter unfolds. We will follow with some of the characteristics that distinguish the different kinds of I/O interfaces and that one must consider and can use as part of a design. These become important when making trade-offs during the early stages of a design.

### 15.5.1 The Transport Mechanism

The hierarchy given in Figure 15.3 identifies the two major elements of the transport mechanism: the physical level and the interconnection architecture.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_785_0.png)

We have already noted that the physical means by which information is moved can be implemented in a variety of ways. On top of the physical medium is the interconnection architecture or topology. The choice of interconnection topology and architecture can have a significant effect on the performance (generally in time), reliability, and economic cost of a system.

#### 15.5.1.1 The Interconnection Topology

An important consideration in the design of the physical medium is its organizational topology. In the local device model, such a medium implements an extension of one of the familiar bus architectures; in the remote device model, the medium is more often called a network. Whichever name is used, however, the intent is the same.

bus network

Star Ring, Parallel Bus

Among the vast number of ways of configuring the interconnection, in general one finds three fundamental organizations. These are the Star (illustrated in Figure 15.4), the Ring (given in Figure 15.5), and the simple Parallel Bus (shown later in Figure 15.8). The architecture of the transport mechanism in most commodity embedded systems modifies or extends one or more of these in some way. We have already looked at different aspects of these bus topologies in other contexts. Some of the material presented here will repeat parts of those discussions.

Each configuration has certain advantages and disadvantages. For all configurations, there are three kinds of messages:

- Those addressed to a single device (point to point).
- Those addressed to a subset of the devices (multicast).
- Those sent to all devices (broadcast).

Each of these configurations can find application in a (wired) local context, such as a collection of microprocessors in a contemporary automobile, within a complex integrated circuit, or in a highly distributed wireless or networked system of Internet appliances. As we look at each of the three major topologies, we will present a high-level description of information flow and fault tolerance. We begin with the star configuration.

#### 15.5.1.2 Star

The star configuration, illustrated in Figure 15.4, is a master–slave type of arrangement. Device-to-device communication must go through the master. The transmit and receive operations proceed as follows.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_786_0.png)

##### 15.5.1.2.1 TRANSMIT FROM MASTER TO SLAVE

The device designated as the master resides at the center of the system; this will typically be the local system. The slave units are any of a variety of peripheral devices. All communication, which typically follows a command–response protocol, must originate from the master, which initiates and directs all the activities within the system and coordinates any message exchange with other devices.

Transactions are typically read or write operations. A write operation sends information to the slave, and the read operation requests that information be returned.

##### 15.5.1.2.2 RECEIVE FROM SLAVE TO MASTER

The transaction is initiated by a request from the master through the issuance of a read command. That command may be used to request status information, perhaps the result of a self-test or the retrieval of the results of some earlier requested operation.

