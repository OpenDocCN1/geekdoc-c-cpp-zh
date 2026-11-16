![](bbox=[0.21, 0.09, 0.86, 0.63])

FIGURE 5-16 The Cortex-M3 memory address space.

For example, if bit 3 at address 2000100016 is to be modified, the bit-band alias is calculated as:

```
2200000016 + 12816 × 100016 + 4 × 3 = 2208000C16
```

Address 2208000C allows direct access to only bit 3 of the word at address 20001000. A read from that address will provide a word of all zeroes except for the least significant bit, which is a copy of the selected bit from the bit-band region. A write to the same address will ignore all but the least significant bit of the data that is written (Figure 5-17).