The basic specification of the DS18B20 is:

+   - Measures temperatures from -55°C to +125°C (-67°F to +257°F)
- ±0.5°C accuracy from -10°C to +85°C
- Thermometer resolution is user-selectable from 9 to 12 Bits
- Converts to 12-bit digital word in 750ms (max)

It can also be powered from the data line, making the bus physically only two wires - data and ground - however this "parasitic power" mode is difficult to make work reliably and best avoided in an initial design. In normal powered mode there are three connections:

![](bbox=[0.446, 0.306, 0.503, 0.473])

Ground needs to be connected to the system ground, $V_{DD}$ to 3.3V and DQ to the pull-up resistor of an open collector bus.

![](bbox=[0.157, 0.566, 0.783, 0.676])

There can be multiple devices on the bus and each one has a unique 64-bit laser ROM code, which can be used as an address to select the active devices. For simplicity, it is better to start off with a single device and avoid the problem of enumerating the devices on the bus, although once you know how everything works this isn't difficult to implement.