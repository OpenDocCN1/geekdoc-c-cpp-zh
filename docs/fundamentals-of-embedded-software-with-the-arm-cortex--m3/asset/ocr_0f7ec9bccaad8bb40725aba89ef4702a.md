| Addr. | Data | Restriction | Description |
| :--- | :--- | :--- | :--- |
| 0020 | xxxx1xxx | Read-Only | Interrupt request or in-service register |
| | xxx0xxxx | Write-Only | Initialization command word 1 (ICW1) |
| | xxx0xxxx | Write-Only | Operation Control Word 2 |
| | xxx01xxx | Write-Only | Operation Control Word 3 |
| 0021 | | Write-Only | Operation Control Word 1 (Interrupt mask register) ICW1, ICW2, ICW3, ICW4 (in order, only just after writing ICW1) |
| 0022-003F | | | Reserved |

```
void InitializeICWs(uint8_t icw[])
{
    bool was_enabled ; // Used to save the current interrupt enable state

    icw[0] = (1 << 4) ; // Bit 4 must be 1 to write ICW1
    was_enabled = GetInterruptEnable() ; // Get current interrupt enable state
    DisableInterrupts() ; // Sequence must not be interrupted!
    BytePort(icw[0], 0x20) ; // Output ICW1 and reset ICW counter
    BytePort(icw[1], 0x21) ; // Output ICW2
    BytePort(icw[2], 0x21) ; // Output ICW3
    BytePort(icw[3], 0x21) ; // Output ICW4
    if (was_enabled) EnableInterrupts() ; // Restore interrupt enable state
}
```

FIGURE 4-10 Function to initialize the four ICW values of the 8259 chip.

# 4.5.4 I/O Devices Differentiated by Bits in the Written Data

Table 4-9 shows that reads from I/O address 0020 access the read-only interrupt request/in-service register, while writes to the same address select one of the write-only registers ICW1, OCW2, and OCW3, according to the value of bits 3 and 4 in the data that is written. For example, writing 01010111 to port 0020 sends the data to ICW1, while writing 01000111 to the same port sends the data to OCW2.

# 4.6 ACCESSING MEMORY-MAPPED I/O DEVICES

Modern microprocessors are capable of addressing gigabytes of memory, yet embedded systems typically need significantly less than a megabyte. If the hardware is designed to assign some of the unused addresses to I/O devices, we can then manipulate their “memory-mapped” I/O ports as if they were memory locations. For example,