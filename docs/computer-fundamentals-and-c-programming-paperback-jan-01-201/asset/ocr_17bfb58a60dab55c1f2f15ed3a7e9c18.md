output in register R3. The contents of R3 would eventually be moved to RAM before the next instruction is read in.

> > **Note:** Prior to this section, we used the term *primary memory* to represent RAM. This section redefines it to signify the memory that is directly connected to the CPU, irrespective of whether it is volatile or not. Contemporary usage of this term is consistent with the one pursued here.

# ## 1.10 SECONDARY MEMORY

The computer also supports *secondary memory*, also known as *secondary storage* or *auxiliary memory*. This memory type is not directly connected to the CPU but it can exist both in the machine or external to it. Secondary memory is non-volatile and thus meets the requirements of offline and long-term storage. These devices are slower than primary memory but they have larger capacities. They are also way cheaper than primary memory; 1 GB of hard disk space is much cheaper than 1 GB of RAM.

The last couple of decades have seen the emergence of multiple types of storage devices. They have different physical sizes and capacities and may or may not require power. In this section, we consider the following storage devices with their typical capacities indicated in parentheses:

+   - Hard disk including the portable disk (500 GB to 4 TB).
+   - Magnetic tape (20 TB).
+   - CD-ROM (700 MB—less than 1 GB).
+   - DVD-ROM (4.7 GB and 8.5 GB).
+   - Blu-ray disk (27 GB and 50 GB).
+   - Flash memory based on the EEPROM (1 GB to 128 GB).
+   - The obsolete floppy disk (1.2 MB and 1.44 MB).

Some of these devices may be part of the computer's configuration, while others may be connected to it through ports and connectors. Even though these devices are meant for offline storage, a program in execution often needs to access them. A program may, for instance, read data from a CD-ROM and write the output to flash memory. Further, the data in these devices are organized in *files* unlike in primary memory where they are arranged contiguously.

> > **Takeaway:** Data in secondary memory is accessed by the name of the *file* associated with the data. On the other hand, data in primary memory is accessed by the addresses of the memory locations containing the data.

# ### 1.10.1 The Hard Disk

Also known as *hard drive* or *fixed disk* because it is fixed inside the computer, the *hard disk* represents one of the oldest but most commonly used forms of secondary storage. Hard disks have very high capacities with the cheapest cost. It is common for a laptop to have 500 GB of storage. Desktops