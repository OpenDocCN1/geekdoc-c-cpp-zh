# SEGMENTATION

# 171

and thus uses the heap base and bounds. Let's take our example virtual address from above (4200) and translate it, just to make sure this is clear. The virtual address 4200, in binary form, can be seen here:

```
13 12 11 10 9 8 7 6 5 4 3 2 1 0
0 1 0 0 0 0 0 0 1 0 1 0 0 0
      Segment Offset
```

As you can see the picture, the two bits (01) tell the hardware which segment we are referring to. The bottom 12 bits are the offset into the segment: 0000 0110 1000, or 0x068, or 104 in decimal. The hardware simply takes the first two bits to determine which segment register to use, and then takes the next 12 bits as the offset into the segment. By adding the register to the offset, the hardware arrives at the physical address. Note the offset eases the bounds check: we can simply check if the offset is less than the bounds; if not, the address is illegal. Thus, if base and bounds were arrays (with one entry per segment), the hardware would be doing something like this to obtain the desired physical address:

```
// get 2 bits of 14-bit VA
Segment = (VirtualAddress & SEG_MASK) >> SEG_SHIFT
// get offset
Offset = VirtualAddress & OFFSET_MASK
if (Offset != Bounds[Segment])
    Raise(PROTECTION_FAULT)
else
    PhysAddr = Base[Segment] + Offset
    Register = AccessMemory(PhysAddr)
```

In our example, we can fill in values for the constants above. Specifically, SEG_MASK would be set to 0x3000, SEG_SHIFT to 12, and OFFSET_MASK to 0xFFFF.

You may have noticed that when we use the two bits, we have only three segments (code, heap, stack), one of the segment space goes unused. To fully utilize the virtual address space (and avoid an unused segment), some systems use only one bit to select which segment [LL82].

Another issue with using the fixed-many bits to select a segment is that it limits the use of the virtual address space. Specifically, each segment is limited to a maximum size, which in our example is 4KB (using the two bits to choose segments implies the 16KB address space gets chopped into pieces, or 4KB in this example). If a running program wished to grow a segment (the heap, or the stack) beyond that maximum, the program is out of luck.

There are other ways for the hardware to determine which segment a particular address is in. In the implicit approach, the hardware deter

© 2008–19, ARPACI-DUSSEAU

THREE
EASY
PIECES