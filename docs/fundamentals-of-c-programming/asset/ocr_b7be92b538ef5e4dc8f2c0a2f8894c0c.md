# Chapter 13

# Standard C++ Classes

In the hardware arena, a desktop computer is built by assembling

+   - a motherboard (a circuit board containing sockets for a processor and assorted supporting cards),
+   - a processor,
+   - memory,
+   - a video card,
+   - an input/output card (USB ports, parallel port, and mouse port),
+   - a disk controller,
+   - a disk drive,
+   - a case,
+   - a keyboard,
+   - a mouse, and
+   - a monitor.

(Some of these components like the I/O, disk controller, and video may be integrated with the motherboard.)

The video card is itself a sophisticated piece of hardware containing a video processor chip, memory, and other electronic components. A technician does not need to assemble the card; the card is used as is off the shelf. The video card provides a substantial amount of functionality in a standard package. One video card can be replaced with another card from a different vendor or with another card with different capabilities. The entire computer will work with either card (subject to availability of drivers for the operating system) because standard interfaces allow the components to work together.

Software development today is increasingly component based. Software components are used like hardware components. A software system can be built largely by assembling pre-existing software building blocks. C++ supports various kinds of software building blocks. The simplest of these is the function that we investigated in Chapter 8 and Chapter 9. A more powerful technique uses built-in and user designed software objects.