# Summary

+   Making SPI work with any particular device has four steps:
1. Discover how to connect the device to the SPI pins. This is a matter of identifying pinouts and mostly what chip selects are supported.
2. Find out how to configure the SPI bus to work with the device. This is mostly a matter of clock speed and mode.
3. Identify the commands that you need to send to the device to get it to do something and what data it sends back as a response.
4. Find, or work out, the relationship between the raw reading, the voltage and the quantity the voltage represents.

+   The MCP3000 range of A-to-D converters is very easy to use via SPI.

+   You can read data at rates as fast as 20kHz, which is fast enough for some audio applications.