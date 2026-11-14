We employ and test the functionality of not only the overarching uCLinux system, but also the uCLinux bootloader, Universal Asynchronous Receiver/Transmitter (UART) communication systems, CPU data and instruction cache, and SRAM and flash memory as both storage devices and as file systems. The end result is a MicroBlaze/uCLinux-based stand-alone system with many paths for future development.

# 19.8.2.2 Requirements

The uCLinux OS was required to control most peripherals on the Spartan III™ development board, including light-emitting diodes (LEDs), UARTs, LCD, flash memory, and SDRAM. The implementation of uCLinux interacted with other PCs via RS232, accepted input, and provided output.

The OS had to be able to add new input and output paths to the maximum capacity of the development environment. The uCLinux kernel and boot loader were required to reside on the flash memory, thereby allowing the OS to boot from a local memory system (flash) rather than relying on re-download of OS on power cycle.

The principal job of the OS was to mediate the interaction of all of the components in the system (including user interface, display, networking, and communication components) and to orchestrate safe handling of shared memory resources.

# 19.8.2.3 System Description

The system configuration for the LATS is given in Figure 19.19.

![](bbox=[0.255, 0.475, 0.895, 0.855])

Figure 19.19 LATS System High-Level Architecture