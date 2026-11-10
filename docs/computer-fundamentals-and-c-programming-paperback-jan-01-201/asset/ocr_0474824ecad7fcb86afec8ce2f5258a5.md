![](bbox=[0.121, 0.123, 0.878, 0.443])

**FIGURE 2.2** Role of the Device Driver

but the systems programmer knows how to *implement* the call in the driver software. Programming a device thus needs detailed knowledge of the device internals, the reason why device drivers are normally written by the device manufacturer.

Instead of having a separate program for driving a device, doesn’t it make sense to include the code for it in the OS or the application? No, because if the device changes, the OS and all applications using it would need to be changed as well. The outcome would then be a programmer’s nightmare. Applications must be independent of the type of hardware they access. Keeping the device driver separate from the OS and programs allows a driver to be shared between multiple programs.

That said, it is true that operating systems include built-in drivers for some commonly used devices. You don’t need a separate driver for attaching flash memory. But even if the OS contains a driver for a device, you should install the (possibly) updated version that is shipped with the product. The newer version would contain improved features and fixes for bugs encountered in previous versions. If you can’t locate the media containing the driver, get the driver software from the Web site of the device manufacturer.

**Takeaway:** Even though the operating system shields the programmer from knowledge of the hardware, it’s the device driver that completely knows the hardware. The OS manages the call it makes to the driver and the response it receives from it.

**Caution:** A driver is meant for a specific model of the device and a specific version of the operating system. Installing a wrong driver may damage the hardware or make it behave improperly. It is also possible that the device may not work at all.