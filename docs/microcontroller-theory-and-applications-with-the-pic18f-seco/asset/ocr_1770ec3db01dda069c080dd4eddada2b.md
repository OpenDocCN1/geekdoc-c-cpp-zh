banking scheme. This divides the memory space into 16 contiguous banks (bank 0 through
15) of 256 bytes. Depending on the instruction, each location can be addressed directly by
its full 12-bit address, or an 8-bit low-order address and a 4-bit Bank Pointer (also called
Bank Select Register, BSR).

There are some advantages of using memory banks. Once the Bank Select
Register (4 bits in this case) is initialized with the bank number using instructions, fewer
bits (8 bits in this case) are needed for data memory addresses. The PIC18F data memory
uses memory banks.

Figure 3.1 shows a simplified data memory layout of the PIC18F. In the figure, the
high 4 bits of an address specify the bank number. As an example, consider address 0x105
of segment 1. The high 4 bits, 0001, of this address define the location as in bank 1, and the
low 8 bits, 0x05, specify the particular address in bank 1.

Memories can be categorized into two main types: read-only memory (ROM)
and random-access memory (RAM). As shown in Figure 3.2, ROMs and RAMs are then
divided into a number of subcategories, which are discussed next.

# **Read-Only Memory**
ROMs (Read-Only memories) can only be read, so it is nonvolatile
memory. CMOS technology is used to fabricate ROMs. ROMs are divided into two
common types: mask ROM and Erasable Programmable ROM (EPROM) such as the 2732,
and EAROM (Electrically Alterable ROM) [also called EPROM or E^2PROM (electrically
erasable PROM)] such as the 2864.

Mask ROMs are programmed by a masking operation performed on a chip during
the manufacturing process. The contents of mask ROMs are permanent and cannot be
changed by the user. EPROMs can be programmed, and their contents can also be altered by
using special equipment, called an *EPROM programmer*. When designing a microcontroller
for a particular application, permanent programs are stored in ROMs. Control memories
used to microprogram the control unit are ROMs.

EPROMs can be reprogrammed and erased. The EPROM chip must be removed
from the system before programming. This memory is erased by exposing the chip to
ultraviolet light via a lid or window on the chip. Typical erase times vary between 10
and 20 minutes. The EPROM can be programmed by inserting the EPROM chip into a
socket of the *EPROM programmer* and providing proper addresses and voltage pulses at
the appropriate pins of the chip.

EEPROMs can be programmed without removing the memory from the ROM’s
sockets. These memories are also called *read-mostly memories* (RMMs), because they have
much slower write times than read times. Therefore, these memories are usually suited for
operations when mostly reading rather than writing is performed.

# **Flash Memory**
Another type of memory, called *Flash memory* (nonvolatile), invented
in the mid-1980s by Toshiba, is designed using a combination of EPROM and E^2PROM
technologies. Flash memory can be reprogrammed electrically while embedded on the
board. One can change multiple bytes at a time. An example of flash memory is the Intel
28F020 (256K x 8-bit). Flash memory is typically used in cellular phones and digital
cameras. Note that the PIC18F uses flash memory as its program memory.

# **Random-Access Memory**
There are two types of RAM: static RAM (SRAM), and
dynamic RAM (DRAM). *Static RAM* stores data in flip-flops. Therefore, this memory does
not need to be refreshed. RAMs are volatile unless backed up by battery. The PIC18F uses
SRAM for its data memory.