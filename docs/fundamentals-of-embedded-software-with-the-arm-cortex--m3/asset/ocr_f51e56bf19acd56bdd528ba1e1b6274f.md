| Architecture | Operand (x) | 8-bit CPU | 16-bit CPU | 32-bit CPU |
|---|---|---|---|---|
| Load/Store Architecture: The only instructions that can reference memory are Load and Store. | 8 bits | | | |
| E.g., RISC processors, such as ARM and MIPS | 16 bits | * | | |
| | 32 bits | X | * | |
| | 64 bits | X | X | * |
| Other Architectures: Instructions like Add and Subtract may have memory operands. | 8 bits | | | |
| E.g., CISC processors, such as Intel x86. | 16 bits | * | | |
| | 32 bits | X | * | |
| | 64 bits | X | X | * |

*The table assumes that a single instruction can store a memory operand no larger than the word size of the processor. However, some processors have instructions that can store a double-length operand (e.g., STRD).

# 12.5.2 Read-Only and Write-Only Access

Even if you only want to read the current value of a shared object and are not modifying it, you must still protect the read. On a 16-bit processor, if you simply copy the value of a shared 32-bit long, an interrupt might occur between the copying of the least significant 16 bits and that of the most significant 16 bits. If the interrupt causes the value in the long to be modified, then one half of the copied value will be from before the change and the other half from after. One way to protect against this kind of data corruption when the value is used in several places in a code sequence is to disable interrupts, make a local (private) copy, reenable interrupts, and then use the local copy. This technique is shown in Figure 12-10.

```
extern long shared_variable ;
long private_copy ;
/* make a copy with interrupts disabled */
disable( ) ;
private_copy = shared_variable ;
enable( ) ;
/* subsequent code can use "private_copy" */
/* without fear of data corruption. */
```

FIGURE 12-10 Protecting read-only access to a shared memory object.