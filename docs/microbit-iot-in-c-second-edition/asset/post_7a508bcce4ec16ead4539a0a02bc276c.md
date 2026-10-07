
You can also see that the clock is measured to be 1MHz as promised.

| | | | | | |
|---|---|---|---|---|---|
| 00 | Channel 0 SPI-MOSI | | 170° (CKAA) | | |
| 01 | Channel 1 SPI-MISO | | 170° (CKAA) | | |
| 02 | Channel 2 SPI-CLOCK | | | | | |
| 03 | Channel 3 SPI-ENABLE | | | | | |

If you want to transfer multiple bytes as a single operation then you can manually leave the CS low until all of the transfers are complete. However, how you need to proceed depends on the slave device and you need to read the datasheet.

## Problems

The SPI bus is often a real headache because of the lack of a definitive standard, but in most cases you can make it. The first problem is discovering the characteristics of the slave device you want to work with. In general this is solved by a careful reading of the datasheet or perhaps by some trial and error, see the next chapter for an example.

If you are working with a single slave generally things work once you have the SPI bus configuration correctly. Where things are more difficult if you have multiple devices on the same bus. Typically you will find SPI devices that don't switch off properly when they are not being addressed. In principle all SPI devices should present high impedance outputs, i.e. act as tri-state buffers, when not being addressed, but some don't. If you encounter a problem you need to check that the selected slave is able to control the MISO line properly.

If you need more CS lines then you can allocate more GPIO lines to the job, but these are in short supply. A better solution is to multiplex the GPIO lines to create additional chip selects. For example, you can use standard GPIO lines as chip selects and connect four SPI slaves using a 2-to-4 decoder.

## Summary

- The SPI bus is often problematic because there is no SPI standard
- Unlike other serial buses it makes use of unidirectional connections.
- The data lines are MOSI (master output slave input) and MISO (master input slave output).
- In addition there is a clock line, which is output from the master, and an unspecified number of select lines.
- Data is transferred from the master to the slave and from the slave to the master on each clock pulse arranged as a circular buffer.
- The library provides the basic functions you need to work with the SPI bus and you can test the SPI bus using a simple loopback connection.
- Controlling the CS line in the case of the micro:bit V2 is a problem the transfer function isn't blocking. The solution is to use an event handler.
- Working with a single slave is usually fairly easy, working with multiple slaves can be more of a problem.

## Chapter 11

## A-to-D With The SPI Bus

The SPI bus can be difficult to make work at first, but once you know how the slave works it gets easier. To demonstrate how it is done let's add eight channels of 12-bit A-to-D using the MCP3008.

The microbit has a single analog to digital converter which can be connected to any of the GPIO lines designated as analog pins. Sometimes, however, this isn't enough. The MCP3000 family of A-to-D converters provides a simple low-cost solution. Although the MCP3008 with 8 A-to-D inputs and the MCP3004 with 4 A-to-D inputs at 10-bit precision are the best known, there are others in the family including 12- and 13-bit precision devices with differential inputs at the same sort of cost - $1 to $2.

In this chapter, the MCP3008 is used because it is readily available and provides a good performance, but the other devices in the family work in the same way and could easily be substituted.

## The MCP3008

The MCP3008 is available in a number of different packages, but the standard 16-pin PDIP is the easiest to work with using prototyping board. You can buy it from the usual sources, see Resources on this book's webpage at www.iopress.info. Its pinouts are fairly explanatory:

| CH | Pin | Signal |
|---|---|---|
| CH0 | 16 | VDD |
| CH1 | 15 | VREF |
| CH2 | 14 | AGND |
| CH3 | 13 | CLK |
| CH4 | 12 | DOUT |
| CH5 | 11 | DIN |
| CH6 | 10 | CS/SHND |
| CH7 | 9 | DGND |

As you can see, the analog inputs are on the left and power and SPI connections on the right. The conversion accuracy is claimed to be 10 bits, but how many of these bits correspond to reality and how many are noise depend on how you design the layout of the circuit.

You need to take great care if you need high accuracy. For example, you will notice there are two voltage inputs $V_{DD}$ and $V_{REF}$. $V_{DD}$ is the supply voltage that runs the chip and $V_{REF}$ is the reference voltage that is used to compare the input voltage.

Obviously if you want accuracy $V_{REF}$, which has to be lower than or to $V_{DD}$, should be set by an accurate low voltage source. However, in most applications $V_{REF}$ and $V_{DD}$ are simply connected together and the usual, low-quality supply voltage is used as the reference. If this isn't good then you can use a Zener diode to a precision voltage reference such as the TL431. At the very least, you should add 1µF capacitor between the $V_{DD}$ pin and the $V_{REF}$ pin to ground.

The MCP3000 family implements a type of A-to-D based on successive approximation. The idea is that first a voltage is generated equal to $V_{REF}/2$ and the input voltage is compared to this. If it is lower, the most significant bit is a zero; if it is more or equal, it is a one. At the next step the voltage generated is $V_{REF}/2+V_{REF}/4$ and the comparison is repeated to generate the next bit.

![](img/23976341c92811237b18beea169.png)

You can see that successive approximation fits in well as each bit can be obtained in the time needed to transmit the previous bit. However, the conversion is relatively slow and a sample-and-hold circuit has to be used to keep the input fixed.

The sample-and-hold takes the form of a 1µF capacitor and a switch. The only reason you need to know about this is that the conversion has to be complete in a time that is short compared to the discharge of the capacitor. So, for accuracy there is a minimum clock rate as well as a maximum. Also, to charge the capacitor quickly enough for it to follow the changing voltage it needs to be connected to a low impedance source. In most cases this isn't a problem, but if it is you need to include an op amp.

If you are using an op amp then you might implement an anti-aliasing filter to remove frequencies from the signal that are too fast for the A-to-D to respond. This takes us into the realm of analog electronics and signal processing and out of the scope of this book.

You can also use the A-to-D channels in differential mode to measure the voltage difference. For example, in differential mode you can measure the difference between CH0 and CH1, i.e. what you measure is CH1-CH0. In most cases you want to use all channels in single-ended mode. In principle you can take 200 samples per second, but only at the upper limit of the supply voltage ($V_{DD}$=5V$), falling to 75 samples per second at its lower limit ($V_{DD}$=2.7V).

The SPI clock limits are a maximum of 3.6MHz at 5V and 1.35MHz at 2.7V. The clock can go slower, but because of the problem with the sample and hold mentioned earlier it shouldn't go below 10kHz. How fast we can take samples is discussed later in this chapter.

![](img/23976341c92811237b18beea170.png)

The connection from the MCP3008 to the micro:bit's SPI bus is very simple and can be seen in the diagram below.

The only additional component that is recommended is a 1µF capacitor connected between pins 15 and 16 to ground, mounted as close to the chip as possible. As discussed in the previous section, you might want a voltage reference for pin 15 rather than using the 3.3V supply.

## Basic Configuration

Now we to the configuration of the SPI bus. Taking into account the maximum clock frequencies for the device of 3.6MHz at 5V and 1.35MHz at 2.7V and the need to maintain a minimum clock rate of 10kHz, using the default clock rate of 1MHz seems a reasonable starting point.

From the datasheet the CS to be active low and, by default, the data is sent most significant bit first for both the master and the slave. The puzzle is what mode to use? This is listed in the datasheet if you look really carefully and it can be mode 0 with clock high or mode 3 with clock active. For simplicity we use mode 0. We now have enough information to initialize the slave:

```
spi.format(8, 0);
spi.frequency(1000000);
```

## The Protocol

Now we have the SPI initialized and ready to transfer data, but what data do we transfer?

The bus doesn't have any standard commands or addressing structure. Each device responds to data sent in different ways and sends data back in different ways. You simply have to read the datasheet to find out what the commands and responses are.

Reading the datasheet might be initially confusing because it says what you have to do is send five bits to the slave - a start bit, a bit that selects its operating mode, and a 3-bit channel number. The operating mode is 1 for single ended and 0 for differential. Differential mode uses the channels in pairs to measure the voltage difference between them. In most cases you want to use single ended. So to read Channel 3, i.e. 011, in single-ended mode you would send the slave:

```
1101xxx
```

where x can take either value.

The response from the slave is that it holds its output in a high impedance state until the sixth clock pulse it sends a zero bit on the seventh followed by bit 9 of the data on the eighth clock pulse.

That is, the slave sends back:

- * x x x x x x ø b9
