# I/O DEVICES

![](bbox=[0.203, 0.153, 0.735, 0.463])

the system by PCIe (Peripheral Component Interconnect Express). In this diagram, a network interface is attached to the system here; higher performance storage devices (such as NVMe persistent storage devices) are often connected.

Figure 36.2: Modern System Architecture

# 36.2 A Canonical Device

Let us now look at a canonical device (not a real one), and use this device to drive our understanding of some of the machinery required to make device interaction efficient. From Figure 36.3 (page 446), we can see that a device has two important components. The first is the hardware interface present to the rest of the system. Like a piece of software, hardware must also present some kind of interface that allows the system to control its operation. Thus, all devices have some specified interface and protocol for their interaction.

The second part of a device is its internal structure. This part of the device is implementation specific and is responsible for implementing the abstraction the device presents to the system. Simple devices will have one or a few chips to implement their functionality; more complex devices will include a single CPU, some general purpose memory, and other device-specific chips to get their job done. For example, modern RAID controllers might consist of hundreds of thousands of lines of firmware (i.e., software within a hardware device) to implement its functionality.

2008–19, ARPACI-DUSAU

THREE EASY PIECES