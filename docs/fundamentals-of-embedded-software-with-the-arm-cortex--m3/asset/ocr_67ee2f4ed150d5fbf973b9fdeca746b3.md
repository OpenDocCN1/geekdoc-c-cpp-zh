hardware that decodes a portion of the memory address space for I/O devices instead of memory. Data held in an I/O device may then be accessed via a pointer whose value has been initialized to its address using the techniques described in Section 4.6.

Unfortunately, the situation is usually somewhat more complex: I/O hardware is often designed so that the data is either read-only or write-only. Sometimes multiple I/O devices are assigned to a single address, requiring other techniques to access the specific data of interest. The following sections discuss common strategies for solving these situations.

# 4.5.1 Write-Only I/O Devices

The read-modify-write techniques presented earlier for manipulating bits within variables stored in read-write memory cannot be used with write-only I/O ports such as the parallel printer-control port of a PC (see Figure 4-8). The solution is to keep a copy of the last bit pattern written to the port in a variable. To modify one or more bits in the port without affecting the other bits, apply the read-modify-write techniques (described earlier in this chapter) to the variable, and then copy the resulting value of the variable to the I/O port.

Synchronization between the value in the variable and that in the actual I/O port is critical. The initial value of the variable must match the hardware reset condition of the port, and every modification of the value in the port must be accompanied by a corresponding update of the variable. An effective technique to insure synchronization is to encase all access to the write-only port in a function that also updates the value of the associated variable. Figure 4-9 illustrates one such function and its usage.

```
void LPTIControl(uint8_t bits2set, uint8_t bits2clr)
{
    static uint8_t bits = 0x00 ; // should match hardware reset condition
    if (bits2set != 0 || bits2clr != 0)
    {
        bits |= bits2set ; // Insert 1's as needed
        bits &= ~bits2clr ; // Insert 0's as needed
        Byte2Port(bits, 0x3BE) ; // Copy bits to the printer port
    }
    else bits = 0x00 ; // Reinitialize to hardware reset condition
}

void PulseLPTIDataStrobe(int msec)
{
    LPTIControl(0x01, 0x00) ; // Set data strobe line to 1
    DelayMilliSeconds(msec) ; // Keep at 1 for a short time
    LPTIControl(0x00, 0x01) ; // Clear data strobe line to 0
}
```

FIGURE 4-9 Manipulating bits in a write-only I/O port.