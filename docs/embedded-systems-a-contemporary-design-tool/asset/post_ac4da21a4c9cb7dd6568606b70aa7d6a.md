
![](img/679b8d2d47f1bf86e17aca48f596f5cc_903_0.png)

Figure 18.2 A High-Level Representation of an Early Communication System

## 18.3.2.1 What It Is ...

In addition to the lines for exchanging data, the standard also specified a number of handshaking and status lines. The more familiar are identified in the following box, along with their initial intended purpose.

- TXD. Data transmission line from DTE to DCE.
- RXD. Data transmission line from DCE to DTE.
- DSR. Data Set Ready from DCE to DTE – intended to inform the DTE that the data set has a valid connection, has completed whatever initialization might be necessary, and is ready to engage in a message exchange. If the connection drops during the exchange, this signal is deasserted.
- DTR. Data Terminal Ready from DTE to DCE – intended to inform the DCE that the data terminal has completed whatever initialization might be necessary, is ready to engage in a message exchange, and would like to open a communication channel.
- RTS. Request to Send from DTE to DCE – intended to inform the DCE that the DTE had data to send and for the DCE to do whatever was necessary (dial, ensure carrier, ensure a line, etc.) to effect the communication.
- CTS. Clear to Send from DCE to DTE – intended to inform the DTE that the DCE had done its job and data could now be sent.
- CD. Carrier detect – intended to indicate that a connection has been established and an answer tone has been received from the remote modem.
- SG. Signal ground – the name says it.

## 18.3.2.2 What They Think It Is ...

The contemporary view of an EIA-232-based system appears more like that in Figure 18.3. Observe that the original modems have been replaced by what is now known as a NULL modem. All too often today the CTS, RTS, DTR, and DSR lines are incorrectly used for handshaking. Why is this a problem? Why will data potentially be lost using such a scheme? Let's return to the original question and consider the actual flow of data.

> CTS, RTS, DTR, DSR

Handshaking, which is a type of flow control, is a way for one piece of DTE to synchronize actions or the exchange of data with another piece of DTE. For example, if data is sent to a printer at a rate higher than the printer can handle because of the speed of printing, it will send a signal to the sending device to stop until it catches up. In the EIA-232 specification, signals such as CTS and DSR are sometimes (mis)used to serve that purpose.

> CTS – Clear to Send, DSR – Data Set Ready

![](img/679b8d2d47f1bf86e17aca48f596f5cc_904_0.png)

Figure 18.3 A Contemporary View of an EIA-232 Communication System

The original intent of an asserted signal on the DSR line was to inform the transmitting device that the communications device (typically the modem) was ready to send data, whereas a deasserted signal would indicate the opposite. The line should be asserted following power up (self-tests, other initialization, and establishing a connection) and should remain in that state until the system is powered down. The signal CTS was/is intended to indicate that the transmitting device that it is now OK to send data – that the physical line is intact, that a carrier has been detected, and so on.

## Universal Asynchronous Receiver Transmitter (UART)

Let's examine the exchange process a bit more closely to identify the problems that can arise from using the DSR and CTS signals as part of a handshake protocol. Most EIA-232-based systems use a Universal Asynchronous Receiver/Transmitter (UART) to manage the message interface. Typically, such devices are double buffered to help unburden the sending device. Similarly, on the receiving side, a UART is also used to manage incoming data. Once again, a double buffer is incorporated.

Let's walk through the diagram in Figure 18.4 and count how many characters may be in transit at any time. Starting with the sender, there may be one in the local application that is ready to be sent, two in the transmitting UART's buffers, one in transit, and two in the receiver's buffers for a total of six characters.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_904_1.png)

Figure 18.4 Data Flow Through an EIA-232 Communication System

If the receiving device's I/O driver (which is using the CTS/RTS pair for flow control) finds that data is coming in faster than it can be processed, the driver will deassert the CTS line. If the receiver's I/O driver immediately switches from the receive thread to the process thread to start working with some of the data, it may lose up to six characters that are in transit. A timer may help, but there is still no guarantee; why? To ensure the proper control of data flowing between the sender and the receiver, that control should be incorporated into the exchange protocol in the driver software.

## 18.3.3 EIA-232 Addressing

Because the original focus of the RS-232 interface was the exchange between a single piece of DTE and a single piece of DCE, addressing was unnecessary. Addressing at a higher level between systems connected through modems to the telephone system occurred naturally through the corresponding telephone numbers.

Today, the vast majority of EIA-232 interfaces use neither a modem nor the telephone system. Consequently, source and destination addressing must be implemented as part of the message exchange protocol utilized by the specific application. The standard makes no provision for such addressing.

## 18.3.4 Asynchronous Serial Communication

The EIA-232 standard utilizes an asynchronous communication scheme. Asynchronous communication recognizes and accepts that there are irregular intervals between the sending of pieces of data.

To help clarify the operation, suppose that a serial communication line is set up to transmit American Standard Code for Information Interchange (ASCII) characters as typed by a person at a keyboard. The spacing between the transmissions of successive characters will naturally vary widely and there may be long periods when no characters are typed or sent. In such a situation, the receiving device needs to determine when a character is being sent to prepare it to receive that character and sort out which part is data, which part is the error-checking field, and so on ... or even if it is a legitimate piece of data rather than noise.

This is accomplished by a process known as framing. In the context of EIA-232 data exchange, each character is framed by a start and a stop bit as illustrated in Figure 18.5.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_905_0.png)

The start bit signals that a data character will follow and, thereby, enables the receiving device to temporarily synchronize with the transmitting device. The stop bit signals the end of the data character and provides time for the receiving device to get ready for the next one.

## 18.3.5 Configuring the Interface

Today the EIA-232 interface is implemented either as an integrated component within a microprocessor or microcomputer or externally using a large-scale integrated (LSI)

- USART – Universal Synchronous/Asynchronous Receiver Transmitter

The external device may be a peripheral processor that is a component included in the microcomputer's supporting chip set or a general purpose device that is provided by another vendor.

Whichever method is used, the device must still be configured to ensure that the sender and the receiver are speaking the same language. The typical minimum set of parameters that must be configured are given in the following list.

- Baud rate. A measure of the speed at which a modem transmits data. Often this is incorrectly assumed to be a measure of the number of bits that are transmitted each second. Baud rate is actually a measure of the number of signaling changes or events per second. In the early days of digital communication one baud may have been 1 bit per second; today's technology permits a single event to encode more than one bit. Thus, for example, a modem that is configured to transmit at 9600 baud is actually communicating at 9600 bits per second by encoding 4 bits per signal event.

- Bits per character. A specification of the size of the character being sent. Typical values are 5, 6, 7, or 8 bits per character.

- Parity. A specification of the parity over the character. Typical values are odd, even, or none.

- Number of stop bits. A specification of the number of stop bits to include. Typical values are 1, 1½, or 2. Two stop bits are rarely used today. This value originated with the old teletypes that literally moved the carriage back to the start of each line. This mechanical operation took some time to complete.

## 18.3.6 Data Recovery and Timing

With an asynchronous transmission scheme, the transmitting and receiving devices are each operating on independent local clocks, which are usually designed to operate at 16X, 32X, or 64X the baud rate. Why do we do this?

- start
- stop
- bit timer

EIA-232 data recovery is based on a bit-timing scheme. Such a scheme works as follows. Each character is framed by a start bit and a stop bit. Once the start bit is detected, a bit timer is enabled to begin incrementing at the selected clock rate. The bit timer is designed such that its period is given as:

timer period = clock rate / baud rate

For example, if the clock rate is 16X the baud rate, the period of the counter will be 16.

For 9600 baud, the clock rate should be 16 times that or 153.6 kHz.

- bit timer
- start

Consequently, the bit timer, which has been enabled at the leading edge of the start bit, will reach a count of eight at the center of the first data bit, as illustrated in Figure 18.6.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_906_0.png)
