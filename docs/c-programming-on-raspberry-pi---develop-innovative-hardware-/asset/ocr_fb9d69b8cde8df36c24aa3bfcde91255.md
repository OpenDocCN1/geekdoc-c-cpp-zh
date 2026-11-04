# ## Chapter 8 • SPI Bus Interface

# ### 8.1 • Overview

In the last chapter, we learned how to interface I2C devices to our Raspberry Pi and develop projects using C.

In this chapter, we will be developing projects using the SPI bus (serial Peripheral Interface) with the Raspberry Pi. The SPI bus is one of the commonly used protocols to connect sensors and other devices to microcontrollers. The SPI bus is a master-slave type bus protocol. In this protocol, one device (the microcontroller) is designated as the master, and one or more other devices (usually sensors) are designated as slaves. In a minimum bus configuration, there is one master and only one slave. The master establishes communication with the slaves and controls all activity on the bus.

Figure 8.1 shows an SPI bus example with one master and three slaves. The SPI bus uses three signals: clock (SCK), data in (SDI), and data out (SDO). The SDO of the master is connected to the SDI of the slaves. SDOs of the slaves are connected to the SDI of the master. The master generates SCK signals to enable data to be transferred on the bus. In every clock pulse, one bit of data is moved from master to slave, or from slave to master. The communication is only between a master and a slave, and slaves cannot communicate with each other. It is important to note that only one slave can be active at any one time because there is no mechanism to identify slaves. Thus, slave devices have enable lines (e.g. CS or CE) which are normally controlled by the master. Typical communication between a master and several slaves is as follows:

+   - Master enables slave 1.
+   - Master sends SCK signals to read or write data to slave 1.
+   - Master disables slave 1 and enables slave 2.
+   - Master sends SCK signals to read or write data to slave 2.
+   - The above process continues as required.

![](bbox=[0.273, 0.676, 0.702, 0.839])

Figure 8.1 SPI bus with one master and three slaves

The SPI signal names are also called MISO (Master in, Slave out), and MOSI (Master out, Slave in). Clock signal SCK is also called SCLK and the CS is also called SSEL. In the SPI