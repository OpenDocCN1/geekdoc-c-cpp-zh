# # Programming in Assembly
Part 4: I/O Programming

Many of the external input/output (I/O) devices, such as keypads, solenoids, and relays, attached to embedded systems are typically mechanical. Their response time is characterized by the time required for physical movement, which is orders of magnitude slower than the speed of a computer’s CPU or main memory. Another common I/O device is an analog-to-digital (A-to-D) converter that takes a voltage as input and provides a digital representation of its value for use in computation. Conversion involves executing an algorithm implemented in the hardware of the A-to-D converter, but which still runs much slower than the speed of the computer.

The bottleneck that usually limits the speed of I/O data transfer is the speed of the external device, and the computer must not transfer data faster than the device can process it. A few I/O devices, however, can transfer data at very high rates that require a thorough understanding of the capabilities and limitations of the various options for how a processor performs I/O.

All I/O devices operate asynchronously with respect to the CPU. In other words, the events that determine when an input device has data available or when an output device is ready to accept more data are independent of the CPU. Most I/O programming, therefore, requires quite a bit of “handshaking” between the CPU and the I/O device to coordinate the transfer so that data is transferred reliably.

The time behavior of I/O data transfer varies considerably from one device to another as shown in Figure 8-1. For example, a keypad provides data at a very low rate and with data bytes arriving at somewhat random times. Data received by a modem arrives at a relatively low rate, but with a reasonably constant time between bytes (periodic). High data rate devices sometimes transmit an entire “block” of several bytes at once. The size of the block may be fixed or variable and, as with slower devices, blocks may arrive randomly or periodically.

| Data Rate | Occurrence | Increasing Time → |
| :--- | :--- | :--- |
| Low | Random | ↓ ↓ ↓ ↓ ↓ ↓ ↓ |
| | Periodic | ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ |
| High | Random | ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ |
| | Periodic | ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓ |

FIGURE 8-1 Different types of time behavior in I/O data transfers.