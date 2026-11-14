![](bbox=[0.273, 0.102, 0.796, 0.477])

Figure 18.8 Universal Serial Bus Network Architecture

**Application** On the host side, the block labeled Application contains the software drivers that provide the application programmer's interface (API) to the USB-hosted device, as well as the means to communicate with the application interface on the client side via the Host Controller. **Host Controller** On the client side, the Application block observes the drivers for the physical device and the interface to the USB level below. Observe that on the host side the middle two layers are logically split into two components: one that provides the interface to the layer above and one that provides the interface to the layer below.

# 18.4.3 The Universal Serial Bus Protocol

All transactions in the USB system originate on the host side. The design does not support interrupts from client devices. On the host side, the USB client initiates an exchange when it calls the USB driver and requests a transfer. The client drivers supply a memory buffer that is used to store data when sending to or receiving from the peripheral device. Each exchange between an endpoint on the client side and the client driver takes place via a communication pipe that is established by USB system software during device configuration. Such a pipe implements a connection-oriented communication scheme.

+   - **communication pipe** When the client wishes to perform a transfer to/from an endpoint, it invokes the USB driver to initiate the transfer by issuing an IO Request Packet (IRP). When the IRP is received by the USB driver, it organizes the request into individual transactions that are executed during a series of 1-ms frames. The driver sets up the transactions based
+   - **USB driver, IO Request Packet (IRP) frames**