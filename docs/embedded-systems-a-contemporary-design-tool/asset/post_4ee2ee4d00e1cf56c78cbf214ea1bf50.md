
### 15.5.1.2.3 TRANSMIT/RECEIVE FROM ONE SLAVE TO ANOTHER

Transmission from one slave device to others is somewhat uncommon in star configurations. The exchange can be executed in several ways. One approach requires that the master act as the intermediary. Information moves from the source device to the master and then from the master to the destination device. The shortcomings of such a scheme are pretty clear. An alternative approach requires that the master configure the exchange by designating one slave device as the source and the other(s) as the destination(s). Thence, the master authorizes the exchange to begin and waits until it completes.

### 15.5.1.2.4 FAILURE

If one device or link fails, communication with others can continue, although system performance may be/is degraded; the services of the failed slave device are lost, however. In contrast, loss of the master represents a potential single-point failure unless a replacement or backup scheme has been incorporated.

### 15.5.1.3 Ring

Variants on the ring are common in communication networks. We find it to be the basis for token ring networks, for networks of embedded processors in an automobile or aircraft, or within a system or network on a chip type of designs. Typically, there is no bus master, and all devices are considered equal. The basic configuration is presented in Figure 15.5. A more robust configuration utilizing two concentric rings is also presented.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_787_0.png)

Figure 15.5 The Ring Network Architecture

addressed Each device accepts all messages circulating in a ring. If a device receiving a message is the addressed device, the message is accepted; otherwise, the message is passed on to the next device on the ring.

### 15.5.1.3.1 TRANSMIT-RECEIVE

Because there is typically no bus master to control access to the bus and because all devices are considered equal, a protocol must be established and used to decide who is able to transmit messages and to use the bus.

readers, writers Referring back to an earlier discussion of shared resources, the bus, in the ring, is a critical and shared resource. We learned from the readers and writers problem that we can permit multiple readers but only a single writer. Access to the ring bus is a readers and writers problem.

Any device can read – receive messages – from the bus. However, only one writer is permitted. One approach that is commonly used to ensure that there is only a single writer is to have a special message or packet called a token continually circulating in the ring. A device is only able to write when it has the token. When it finishes writing, it releases the token and the process continues.

Another approach that is used is to implement a collision detection/retransmit scheme. The underlying premise is that attempts at access are occurring randomly. Thus, when a device wants to transmit, it first checks for activity on the bus. If it does not see any activity, it puts its data onto the bus and looks for a collision (someone else may have had the same idea). If it detects a collision, it ceases transmission and waits (backs off) a random amount of time before repeating the process. With a lightly loaded bus or bursty transmissions, the probability of repeated collisions is small. We will see several alternative approaches for dealing with collisions when we study the I²C and Controller Area Network (CAN) buses in Chapter 16.

### 15.5.1.3.2 FAILURE

The ring can provide a very robust context for information exchange. Consider first the single ring given in Figure 15.6. If either of the failures shown in the accompanying drawing occurs, the system can reconfigure itself into a parallel bus that will be discussed next. In the event of a link failure (X on the link), full connectivity and communication with all devices on the network can be maintained. If a device (X on the node) is lost, the system has the same degraded performance encountered with the master–slave configuration.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_788_0.png)

Figure 15.6 Basic Ring Architecture with a Single Failure

When implemented as two concentric rings, as in Figure 15.7, there are several possible failure and recovery modes. If one link is lost, as shown with failures numbered as 1 or 2, the system can reconfigure to a fully operational single-link system. If two links are lost, as depicted with the failure numbered 3, once again, the system can reconfigure into a fully operational single-link topology. If a device is lost, as reflected with the failure designated 4, the remaining devices are still fully interconnected via a single-ring configuration. The double ring is also tolerant of second failures. Observe that failure 1 followed by 2 leaves a fully operational system. Other combinations follow with varying levels of degraded performance.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_789_0.png)

Figure 15.7 Dual-ring Architecture with Multiple Failures

### 15.5.1.3.3 PARALLEL BUS

The traditional bus, shown in Figure 15.8, is a variation on the star architecture. There may or may not be a bus master. The SCSI (Small Computer Systems Interface) subsystem in the familiar program counter (PC) is a design that uses a master device called a controller.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_789_1.png)

Figure 15.8 Parallel Bus Architecture

Such a simple bus is probably one of the more commonly used architectures. Device interconnection occurs in a variety of different ways. Generally, all devices can receive information whether it is data and commands or simply commands. The ability to transmit may be more restricted, with some devices being designated as receive only.

As encountered with the ring configuration, the problem of controlling access to the bus for transmit operations must be addressed. Alternatives range from those already discussed with the star topology – designating a bus master – to variants on the token schemes, to the implementation of a control bus to coordinate all transactions to the implementation of a request/grant protocol.

### 15.5.1.3.4 TRANSMIT-RECEIVE

If there is a bus master, the protocol follows the one discussed in a similar context earlier. The information exchange may be point to point, broadcast, multicast, or polled. All devices can listen for and act on a message.

### 15.5.1.3.5 FAILURE

Failure modes and effects follow those discussed for the star configuration. An individual device failure will not compromise the bus – assuming proper isolation. However, a severed bus can prevent communication beyond the damage.

## 15.5.2 Control and Synchronization

The control and synchronization aspects of the extended model of interprocess communication are characterized by:

- The flow of information.
- The I/O timing.
- The software drivers that manage the exchange.

The relationship among these is captured in Figure 15.9. Note that the control and synchronization component sits on top of the transport mechanism.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_790_0.png)

Shortly we will consider how local and remote exchanges can be expressed. At that point, we will see that the lower level aspects of control and synchronization will be unique to each type of exchange. For the moment, the analysis that follows applies to both.

## 15.5.3 Information Flow

Managing the movement of information includes controlling two aspects of the transport process: the direction of the flow and the magnitude of the flow. We will first consider flow direction.

### 15.5.3.1 Direction of Flow

If information is being sent in one direction only – sender to receiver or receiver to sender – the transportation is called *simplex*. If information is permitted to flow in both directions, but in only one direction at a time, it is called *half duplex*. If the exchange supports flow in both directions, possibly simultaneously, it is designated as *full duplex*. Figure 15.10 shows each scheme.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_790_1.png)
