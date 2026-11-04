![](bbox=[0.18, 0.13, 0.85, 0.42])

Figure 14.14 Block diagram of the project

# Circuit diagram:

The circuit diagram of the project is shown in Figure 14.15. LED0 and LED1 are connected to GPIO 21 and 20 of the Raspberry Pi through 470 Ohm current limiting resistors respectively.

![](bbox=[0.32, 0.7, 0.82, 0.86])

Figure 14.15 Circuit diagram of the system

# HTTP Web server/client

A web server is a program that uses HTTP (Hypertext Transfer Protocol) to serve web pages to users in response to their requests. These requests are forwarded by HTTP clients. By using the HTTP server/client pair, we can control any device connected to a web server processor over the web.

Figure 14.16 shows the structure of a web server/client setup. In this figure, the Raspberry Pi is the webserver and the PC (or a laptop, tablet, or mobile phone) is the web client. The device to be controlled is connected to the webserver processor. In this example, we have