![](bbox=[0.23, 0.08, 0.9, 0.29])

# Figure 18.3 A Contemporary View of an EIA-232 Communication System

The original intent of an asserted signal on the DSR line was to inform the transmitting device that the communications device (typically the modem) was ready to send data, whereas a deasserted signal would indicate the opposite. The line should be asserted following power up (self-tests, other initialization, and establishing a connection) and should remain in that state until the system is powered down. The signal CTS was/is intended to indicate that the transmitting device that it is now OK to send data – that the physical line is intact, that a carrier has been detected, and so on.

# Universal Asynchronous Receiver Transmitter (UART)

Let's examine the exchange process a bit more closely to identify the problems that can arise from using the DSR and CTS signals as part of a handshake protocol. Most EIA-232-based systems use a Universal Asynchronous Receiver/Transmitter (UART) to manage the message interface. Typically, such devices are double buffered to help unbunden the sending device. Similarly, on the receiving side, a UART is also used to manage incoming data. Once again, a double buffer is incorporated.

Let's walk through the diagram in Figure 18.4 and count how many characters may be in transit at any time. Starting with the sender, there may be one in the local application that is ready to be sent, two in the transmitting UART's buffers, one in transit, and two in the receiver's buffers for a total of six characters.

![](bbox=[0.25, 0.66, 0.9, 0.8])

# Figure 18.4 Data Flow Through an EIA-232 Communication System

If the receiving device's I/O driver (which is using the CTS/RTS pair for flow control) finds that data is coming in faster than it can be processed, the driver will deassert the CTS line. If the receiver's I/O driver immediately switches from the receive thread to the process