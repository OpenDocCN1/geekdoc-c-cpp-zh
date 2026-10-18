![](bbox=[0.15, 0.13, 0.85, 0.63])

# FIGURE 7.8

Comparison of send/receive and SCIF RMA APIs for data transfer.

+   - scif_send and scif_recv: These APIs are simple to use but are not meant to be very efficient. As shown by “A” in Figure 7.8, transferring data using these APIs involves ring transitions on both the send and receive sides, several memory copies as well as interrupts across PCIe.

+   - scif_(v)writeto and scif_(v)readfrom: These APIs use the DMA engines (see “B” in Figure 7.8) to transfer data from one end to the other. While they provide the highest bandwidth path and free up the CPU to do something else in the meantime, this method of transfer incurs the overhead of programming DMA descriptors (2) and handling interrupts (3). In addition, programming the DMA block of hardware is done in the kernel mode driver that involves a ring