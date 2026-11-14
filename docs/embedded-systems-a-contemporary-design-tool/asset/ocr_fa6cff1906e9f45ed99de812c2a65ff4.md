# 18.3.8 An Implementation

The block diagram in Figure 18.7 gives a typical interface to the external UART-type device. From the microprocessor's point of view, the device can appear either as a memory-mapped I/O device or as a special purpose peripheral processor.

![](bbox=[0.13, 0.19, 0.9, 0.45])

Figure 18.7 Block Diagram for a UART Type Device

In the block diagram, the UART is a peripheral device sitting on the microprocessor bus. The address lines serve the dual purpose of selecting the UART and identifying registers internal to the device that must be written to configure the device. The data lines are bidirectional and contain data that is to be written or transmitted from or received by the UART. Each exchange is accompanied by either an RD strobe to read a received character from the UART or a WR strobe to send one. The Data Rec. line can be either polled or used to generate an interrupt when a character has been received. The Tx Rdy line indicates that the UART's internal transmit buffer is empty and a new character can be transmitted. Like Data Rec., the line can either be polled or used as an interrupt.

# 18.4 THE UNIVERSAL SERIAL BUS – SYNCHRONOUS SERIAL COMMUNICATION

When it is necessary to rapidly transfer larger blocks of regularly spaced data over a significant distance, the overhead of resynchronizing the timing between sender and receiver with each character can become significant. An alternative approach is known as synchronous transmission.

Start and stop bits are no longer needed. Both the sender and receiver are working, directly or indirectly, from a common clock. That clock may exist as a separate signal on the communication channel or it may be encoded in the data using any of the techniques discussed in the previous chapter.