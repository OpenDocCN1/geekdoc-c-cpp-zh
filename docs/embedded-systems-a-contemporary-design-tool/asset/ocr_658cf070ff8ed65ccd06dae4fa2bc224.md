system. One of the major differences is the potential need to manage the refresh function. A second difference results from a memory size versus IC package size difficulty. Today one can easily find numerous variations on the basic DRAM architecture (EDO – Extended Data Output; SDRAM – Synchronous DRAM; FPM – Fast Page Mode). At the end of the day, all of these different types are simply DRAMs. The differences appear in the way that they are organized and how they are accessed. At the root of the differences is the need to accommodate the ever increasing speed of contemporary processors. Thus, the DRAM access is synchronized to the system clock, block access addressing is improved, or pipelined access is permitted. Today, the basic DRAM is referred to as the -regular or conventional DRAM. The newer devices incorporate refresh management inside the device and support a number of other useful features as well.

In the SRAM design, insufficient pins were available on the microprocessor to permit all the necessary address bits to be controlled in parallel. The problem was solved by multiplexing the desired address onto a smaller bus and then demultiplexing it into a full-width address register.

The ability to store large quantities of information in today's DRAMs presents a similar conundrum. Current integrated circuit package technology does not support a sufficient number of I/O pins to simultaneously accommodate the necessary number of address bits. We solve the problem by multiplexing the address into the chip as a row segment and a column segment and then demultiplexing them once they are inside. As we did with the SRAM design, each segment of the address is accompanied by a strobe; for the DRAM these are identified as the RAS and the CAS.

As a basis for understanding contemporary variations on the DRAM, let's abstract away the performance-enhancing modifications and examine the operation of the basic DRAM core. For the current analysis, we will use a 4 M by 16-bit device – a RAM that will store 4 million 16-bit words.

# 4.11.1 DRAM Timing Analysis

# 4.11.1.1 Core Components

To begin the study of the DRAM core and the critical timing elements, some new vocabulary is necessary.

| Term | Description |
| :--- | :--- |
| RAS – Row Address Strobe | Asserts that the row segment of the address is on the input address bus. |
| CAS – Column Address Strobe | Asserts that the column segment of the address is on the input address bus. |
| RAS Cycle Time | Specifies the period of RAS. |
| RAS to CAS Delay | Specifies the separation between the start of a row address strobe and the start of a column address strobe. |
| Refresh Period | Specifies the maximum period in which all memory cells must be refreshed to ensure that no data is lost. |

The relative timing for some of these signals in the base case is illustrated in Figure 4.20.

The timing of the row or column address with respect to the RAS or CAS signals permits either the leading or trailing edge of the strobe to capture the address information.