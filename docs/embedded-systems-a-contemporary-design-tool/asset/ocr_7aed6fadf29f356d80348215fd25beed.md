![](bbox=[0.26, 0.08, 0.85, 0.25])

Figure 18.22 A Block Diagram for a Basic CAN Bus Network

# 18.6.2 Electrical Considerations

Electrically, the CAN bus utilizes balanced differential signaling similar to the approach used by the USB – the current in each signal line is equal and opposite. Such a scheme significantly enhances noise immunity, improves common mode noise rejection, and improves fault tolerance over single-ended drive models. All are essential for the automotive environment in which the bus is designed to operate. dominant, recessive

The two serial lines that make up the CAN bus are designated CANH and CANL. The bus signaling protocol defines two states, dominant and recessive. Similar to the wired AND configuration in the I²C bus, dominant will override recessive. When the transmitted data, TXD, is a logical 0, the bus is in the dominant state; the CANH signal line is taken to 3.5 V and the CANL is taken to 1.5 V, giving a difference of 2.0 V. When the transmitted data is a logical 1, the bus is in the recessive (quiescent) state, which is set to 2.5 V. The timing diagram in Figure 18.23 illustrates the two conditions.

The transmission rates on the bus range from 40 Kbit/s over a 1000 m cable to 1 M bit/s over a 40 m cable. The standard further specifies the maximum stub length off the main bus to be 0.3 m.

![](bbox=[0.2, 0.6, 0.9, 0.86])

Figure 18.23 A Timing Diagram Illustrating Dominant and Recessive Signaling on the CAN Bus