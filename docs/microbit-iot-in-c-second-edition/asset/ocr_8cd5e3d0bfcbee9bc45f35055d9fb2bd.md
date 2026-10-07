# Summary

+   - The 1-Wire bus is a proprietary, but widely used, bus. It is simple and very capable.
- As its name suggests, it makes use of a single data wire and usually a power supply and ground.
- It is possible to dispense with the power line and the connected device will draw power from the data line.
- Implementing the 1-wire bus protocol is mostly a matter of getting the timing right.
- There are three types of interaction: presence pulse, read and write.
- The 1-wire bus protocol is easier to implement than you might think because each bit is sent as a "slot" and, while timing is critical within the slot, how fast slots are sent is not.
- As you can't switch a line from output to input fast enough, you have to use two GPIO lines to implement the 1-Wire bus, unless you are prepared to work directly with the hardware.
- The DS18B20 temperature sensor is one of the most commonly encountered 1-Wire bus devices. It is small, low-cost and you can use multiple devices on a single bus.
- After a convert command is sent to the device, it can take 750ms before a reading is ready. When the data is ready you can read the scratchpad memory where the data is stored.
- If you program the hardware directly you can use a singe GPIO line to implement the 1-Wire bus protocol.