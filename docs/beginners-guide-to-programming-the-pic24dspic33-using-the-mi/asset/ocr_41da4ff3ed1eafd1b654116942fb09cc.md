Besides the 8 data bits an error correction or parity can be sent (optional). The final part of the communication is a stop bit which occurs when the serial communication line is fixed high for one or two bits times (size is optional as well), after parity. See Figure 7-1 below.

Note for this communication to work each transmitter output line must be tied directly to a receiver input line. Specifically, side one’s transmitter must be tied to side two’s receiver and side two’s transmitter must be tied to side one receiver (if communication is to occur in both directions).

When only one UART is allowed to transmit its data traffic at a time the communications is designated “half-duplex”. However, when the configuration allows for both UARTs to simultaneously transmit data, the communication is termed “full-duplex”.

# Serial Communications

![](bbox=[0.159, 0.425, 0.912, 0.719])

Figure 7-1 UART Semi-Asynchronous Communication

The UART naturally extends to wireless as well as wired communications. Figure 7-2 shows a UART in a wireless application. Wireless transmitters typically share the same carrier frequency forcing the communications to be half-duplex (only one transmitter on at a time). This insures that the communication avoid data collisions. Coordination of communication is done typically with use of a “higher layer” software protocol that resides over this “lower layer” data link to establish who can talk and when.