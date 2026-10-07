# 240 PAGING: SMALLER TABLES

```
VPN = (VirtualAddress & VPN_MASK) >> SHIFT
(Success, TlbEntry) = TLB_Lookup (VPN)
if (Success == True) // TLB Hit
    if (CanAccess(TlbEntry.ProtectBits) == True)
        Offset = VirtualAddress & OFFSET_MASK
        PhysAddr = (TlbEntry << SHIFT) | Offset
        Register = AccessMemory(PhysAddr)
    else RaiseException(PROTECTION_FAULT)
else // TLB Miss
    // first, get directory entry
    PDIndex = (VPN & PD_MASK) >> PD_SHIFT
    PDEAddr = PDBR + (PDIndex + sizeof (PDE))
    PDE = AccessMemory(PDEAddr)
    if (PDE.Valid == False)
        RaiseException(SEGMENTATION_FAULT)
else
    // if valid, fetch PTE from page table
    PTIndex = (VPN & PT_MASK) >> PT_SHIFT
    PTEAddr = (PDE << SHIFT) + (PTIndex * sizeof (PTE))
PTE = AccessMemory(PTEAddr)
    if (PTE.Valid == False)
        RaiseException(SEGMENTATION_FAULT)
else if (CanAccess(PTE.ProtectBits) == False)
        RaiseException(PROTECTION_FAULT)
else
    Tlb_Insert (VPN, PTE.PFN, PTE.ProtectBits)
RetryInstruction()
```

Figure 20.6: Multi-level Page Table Control Flow

next part of the VPN (PD Index 1). Finally, if valid, the PTE address can be formed using the page-table index combined with the second-level PDE. When! That's a lot of work. And all just to look up something in a multi-level table.

# The Translation Process: Remember the TLB

To summarize the entire process of address translation using a two-level page table, we again present the control flow in algorithmic form (Figure 20.6). The figure shows what happens in hardware (a hardware-managed TLB) upon every memory reference.

As you can see from the figure, before any of the complicated multi-level page access occurs, the hardware first checks the TLB; upon a hit, the physical address is formed directly without accessing the page at all, as. Only upon a TLB miss does the hardware need to perform the full multi-level lookup. On this path, you can see the cost of our traditional two-level page table: two additional memory accesses to look up a valid translation.

OPERATING SYSTEMS
[VERSION 1.01]

WWW.OSTEP.ORG