
Furthermore, because the timer is incrementing modulo 16, it will again reach a count of eight by the center of the second and succeeding data bits.

### bit timer

Observe that the Q output of the most significant bit of the bit timer makes a 0 → 1 transition when the count advances from 7 (0111) to 8 (1000). That transition can be used to clock the incoming data into a shift register. The same transition can be used to increment a second bit counter that counts the number of incoming data bits that have been stored.

### bit counter

### bit timer, bit counter start

When the agreed upon (by the sender and receiver) number of bits have been stored, it is known that a full character has been received. Both the bit timer and bit counter return to the quiescent state awaiting the next start bit.

The following are key elements to the approach working properly:

- 1. The sender and receiver must be operating at the same baud rate.
- 2. The sender and receiver must agree on the number of bits comprising a character.
- 3. The quiescent state of the data lines is known. The EIA-232 standard specifies this to be the logical 1 state.
- 4. The sender must place the data line into the quiescent state for at least one bit time between characters. This time is known as the stop bit.

The major advantage of the technique is that the sampling signal does not have to be decoded from some counter state, and, thus, cannot have any decoding spikes. Furthermore, by sampling in the center of each bit, the maximum tolerance for error in bit timing is designed into the receiver. Using such a scheme, we can resynchronize the receiver and transmitter with each character. Although the clocks in the sending and receiving devices are ideally operating at the same frequency, a difference of a percentage point or two in the frequencies should not result in transmission errors.

## 18.3.7 EIA-232 Interface Signals

### Mark space

The EIA-232 data and control signals along with their voltage levels are summarized in Table 18.1. A logical 1, known as a mark, corresponds to a voltage level between −3 and −15 V. A logical 0, or space, corresponds to a voltage level between +3 and +15 V. Such values are intended to improve system noise immunity.

### Table 18.1 EIA-232 Signal Levels

| Notation | Interchange Voltage |
| :--- | :---: |
| | Negative | Positive |
| Binary state | 1 | 0 |
| Signal condition | Marking | Spacing |
| Function | OFF | ON |

The internal logic levels in most contemporary embedded systems remain at the 5.0 VDC level. Consequently, outgoing and incoming EIA-232 signals must be buffered and/or level shifted from or to standard logical levels before they can be used. Finally, note that the data link remains in the marking state (< −3 V) until the start bit, a space (> +3 V), is sent.

## 18.3.8 An Implementation

The block diagram in Figure 18.7 gives a typical interface to the external UART-type device. From the microprocessor's point of view, the device can appear either as a memory-mapped I/O device or as a special purpose peripheral processor.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_908_0.png)

Figure 18.7 Block Diagram for a UART Type Device

In the block diagram, the UART is a peripheral device sitting on the microprocessor bus. The address lines serve the dual purpose of selecting the UART and identifying registers internal to the device that must be written to configure the device. The data lines are bidirectional and contain data that is to be written or transmitted from or received by the UART. Each exchange is accompanied by either an RD strobe to read a received character from the UART or a WR strobe to send one. The Data Rec. line can be either polled or used to generate an interrupt when a character has been received. The Tx Rdy line indicates that the UART's internal transmit buffer is empty and a new character can be transmitted. Like Data Rec., the line can either be polled or used as an interrupt.

## 18.4 THE UNIVERSAL SERIAL BUS – SYNCHRONOUS SERIAL COMMUNICATION

When it is necessary to rapidly transfer larger blocks of regularly spaced data over a significant distance, the overhead of resynchronizing the timing between sender and receiver with each character can become significant. An alternative approach is known as synchronous transmission.

Start and stop bits are no longer needed. Both the sender and receiver are working, directly or indirectly, from a common clock. That clock may exist as a separate signal on the communication channel or it may be encoded in the data using any of the techniques discussed in the previous chapter.

Although synchronous transfer requires less overhead and, therefore, can be much more efficient, its uses are more limited than asynchronous data transfer. Thus, today, asynchronous implementations remain more widely used. This ratio is changing with some of the newer interfaces, such as the USB or FireWire.

The USB provides a good example of a typical synchronous interface. Like the EIA-232 interface, much of the low-level design work has been subsumed in a variety of LSI interface chips. In most cases, one can simply include such devices as part of a design. Nonetheless, it is still important to understand the motivation for the standard as well as the underlying signaling and protocols.

### 18.4.1 Background

The factors leading to the creation of the USB parallel many of the factors that preceded the development of the RS-232 standard. Among these are the cacophony of different interfaces and associated connection schemes, limitations on and conflicts with system I/O resources, and cost.

The goals that the developers set for themselves were rather mundane: any new system should overcome existing shortcomings, and it should provide room for growth and expansion. Such ideas are good to keep in mind at the start of each new design. More specifically, the designers identified the following needs:

- Single connector type.
- Ability to attach many different peripherals to the same connector.
- Method to ease resource conflicts.
- Automatic detection and configuration of peripheral devices.
- Low cost for system and peripheral implementers.
- Enhanced performance capability.
- Support for attaching new peripherals.
- Support for legacy software and hardware.
- Low power implementation – support for green systems.

The ultimate solution did a very good job of addressing each of these needs. In particular, I/O resource limitations and conflicts, once all too common with legacy systems, no longer exist. Each device residing on the USB is assigned an address known only to the USB subsystem and, therefore, does not consume any of the primary system resources. While the upper bound of 127 addresses may pose a limit in some large systems, this should not be a problem in most distributed embedded applications. In addition to the 127 directly accessible addresses, each USB device supports the number of ports called endpoints that can be accessed indirectly.

### 18.4.2 The Universal Serial Bus Architecture

The design and implementation of the USB system follows the Open Systems Interconnection (OSI) and Transmission Control Protocol/Internet Protocol (TCP/IP) network architectures that we studied earlier. The USB uses a three-level hierarchy as shown in Figure 18.8.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_910_0.png)

Figure 18.8 Universal Serial Bus Network Architecture

**Application** On the host side, the block labeled Application contains the software drivers that provide the application programmer's interface (API) to the USB-hosted device, as well as the means to communicate with the application interface on the client side via the Host Controller. **Host Controller** On the client side, the Application block observes the drivers for the physical device and the interface to the USB level below. Observe that on the host side the middle two layers are logically split into two components: one that provides the interface to the layer above and one that provides the interface to the layer below.

### 18.4.3 The Universal Serial Bus Protocol

All transactions in the USB system originate on the host side. The design does not support interrupts from client devices. On the host side, the USB client initiates an exchange when it calls the USB driver and requests a transfer. The client drivers supply a memory buffer that is used to store data when sending to or receiving from the peripheral device. Each exchange between an endpoint on the client side and the client driver takes place via a communication pipe that is established by USB system software during device configuration. Such a pipe implements a connection-oriented communication scheme.

- **communication pipe** When the client wishes to perform a transfer to/from an endpoint, it invokes the USB driver to initiate the transfer by issuing an IO Request Packet (IRP). When the IRP is received by the USB driver, it organizes the request into individual transactions that are executed during a series of 1-ms frames. The driver sets up the transactions based
- **USB driver, IO Request Packet (IRP) frames**
