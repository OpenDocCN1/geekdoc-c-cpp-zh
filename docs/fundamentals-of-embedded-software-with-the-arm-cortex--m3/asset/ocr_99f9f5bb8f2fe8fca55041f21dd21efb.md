18. The hardware of our ARM processor was designed so that exception handlers (including ISRs) could be written in C like any other function. Which registers did this require to be saved on the stack during the hardware response to the interrupt request?

19. Both interrupt-driven I/O and polled waiting loop I/O are implemented in software, yet the maximum data rate of interrupt-driven I/O is almost an order of magnitude slower. What causes this?

20. For input devices, latency is defined as the time from the moment that data is available at the device until the time that the data is read from the device. What determines latency when:

+   (a) Interrupt-driven I/O is used, interrupts are enabled, and no other ISRs are currently executing?
+   (b) Interrupt-driven I/O is used and interrupts are enabled, but other ISRs are currently executing?
+   (c) DMA is used?
+   (d) Polled waiting loop is used?

21. Write an instruction loop that transfers 1,000 bytes of data from one area of memory to another as fast as possible, and estimate how long it will take to execute on a Cortex-M3 with a zero wait-state memory.