To start the translation process, the CPU needs the physical address of the process's PDDT. This is found in the CR3 register where a thread is running. You can display this address by looking at the DirBase field in the output of the !process, as shown here:

```
1kd> !process -1 0
PROCESS 99a3040 SessionId:2 Cid:1690 Peb:03159000 ParentCid:0920
 DirBase:0x0124800 ObjectTable:b3b386c0 HandleCount:<Data Not Accessible>
 Image:wndbg.exe
```

The DirBase field shows that the PDPT is at physical address 0x0124800. As shown in the preceding illustration, the PDPT index field in the virtual address is 0. The PDPT entry contains the physical address of the relevant page directory is the first entry in the PDPT, at physical address 0x0124800.

The kernel debugger !pte command displays the PDE and the PTE that describe a virtual address, as shown here:

```
1kd> !pte 31660004
 VA 03166004
 PDE at 0xC060C060 PTE at 0xC018B30
 contains 000000056238867 contains 800000005de61867
 pfn 56238 --- pfn 5de61 ---UU-V
```

The debugger does not show the PDPT, but it is easy to display its physical address:

```
1kd> !dq 0x0124800 L.4
 # 0124800000000053c88901 0000000053c89801
 # 0124810000000053c8a801 0000000053c8801
```

Here we use the debugger extension command !dq. This is similar to the dq command (display as quad--64 bit) but lets us examine memory by physical rather than virtual address. Because the PDPT is only four entries long, we use L 4 length to keep the output uncluttered.

As illustrated, the PDPT index (the two most significant bits) you want is the first displayed quadword. PDPT entries have a format equal to 0, similar to PDEs and PTEs, so you can see that this one contains a PFN of 0x53c8800 (always page-aligned), for physical address of 0x53c8800. That is the physical address of the page directory.

The !pte output shows the PDE address 0xC060C000 at virtual address, not physical. In x86 systems, the first page directory starts at virtual address 0xC0600000. In this case, the PDE address is 0xC00—that, is, 8 (size of an entry) times 24 to the page directory start address. Therefore, the page directory index of the sample virtual address is 24. That means you're looking at the 25th PTE in the page directory.

The PDE provides the PFN of the needed page entry. In this example, the PFN is 0x5623800, so the page table starts at physical address 0x56238000. Then the MMU will add the page table index (0x166) from the virtual address multiplied by 8 (the size of a PTE in bytes). The result-ing address of the PTE is 0x56238B30.