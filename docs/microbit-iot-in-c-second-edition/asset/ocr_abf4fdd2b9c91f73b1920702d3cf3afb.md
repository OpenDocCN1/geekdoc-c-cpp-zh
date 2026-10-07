# Chapter 12

# Serial Connections

The serial port is one of oldest of ways of connecting devices together, but it is still very useful. The micro:bit has a single serial interface, but it can be directed to use any of the GPIO pins as Rx and Tx. The software that powers the micro:bit does a lot to make the single-tasking environment that it is based on more like a multi-tasking operating system. The facilities it provides for working with the serial interface are extensive and is important to know how it all works because it goes well beyond the raw serial facilities on which it is based.

# Serial Protocol

The serial protocol is very simple - it has to be because it was invented in the days when it was generated using electromechanical components, motors and the like. it was designed to make early teletype machines work and hence you will often find abbreviations such as TTY in connection with. As the electronic device used to work with serial is called a Universal Asynchronous Receiver/Transmitter, the term UART is often used.

The earliest standards are V24 and RS232. However, notice that early communications worked between ±24 and later ±12V. Today serial communications works at logic, or TTL, levels 0 to 5V or 0 to 3.3V. Voltage difference is a problem we will return to. What matters is, irrespective of the voltage, the protocol is always the same.

For the moment let on the protocol, as already mentioned is simple. The line rests high and represents a zero. When the device starts to transmit, it pulls the line to generate a start bit. The width of this bit starts the transmission speed - all bits are the same width as the start bit. After the start there are a variable number, usually seven or eight, data bits, an optional single parity bit and finally one or two stop bits.

Originally the purpose of the start bit was to allow the motors to get started and allowing the receiving end to perform any timing corrections – the start bit determined the width of all subsequent bits. The stop bits were similarly there to give time for the motors to come back to their rest positions. In the early days the protocol was used at very slow speeds - 300 baud, i.e. roughly 300 bits per second, was considered fast enough.