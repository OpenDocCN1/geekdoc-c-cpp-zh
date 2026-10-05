The debugger shows that this PTE is at virtual address 0xC0018B30. Notice that the byte offset (0xB30) is the same as that from the physical address, as is the case in address translation. Because the memory manager maps page tables starting at 0xC0000000, adding 0xB30 to 0xC0018000 (the 0x18 is 24 as you've seen) the virtual address shown in the kernel output: 0xC0018B30. The debugger shows that the PFN field of the PTE is 0x5DE61.

Finally, you can consider the byte offset from the original address. Now, the MMU concatenates the byte offset by the PFN from the PTE, giving a physical address of 0x5DE6104. This is the physical address that corresponds to the original virtual address of 0x3166004...at the moment.

The flags bits from the PTE are interpreted to the right of the PFN number. The PTE that describes the page being has flags of DA--UW-V. Here, A stands for accessed (the page has been read), U for user-mode accessible (as opposed to kernel-mode accessible), W for writable (rather than just read), and V for valid (the PTE represents a valid page in physical memory).

To confirm the calculation of the physical address, look at the memory in question via both its virtual and its physical address. First, using the debugger's dd (display words) command on the virtual address, you see the following:

```
1kd> dd 31666004 L 10
03166004 00000034 00003020 0000004e
03166014 00000000 00020020 000a00a0 00000014
```

And with the !d dd 5DE6104 L 10

```
1kd> dd 5DE6104 L 10
#5DE61004 00000006 00003020 0000004e
#5DE61014 00000000 00020020 000a00a0 00000014
```

You could similarly compare the displays from the virtual and physical addresses of the PTE and PDE.

# x64 virtual address translation

Address translation on x64 is similar to x86, with a fourth level. Each process has a top-level extended page called the page map level 4 table that contains the physical locations of 512 third-level structures, called page directory pointers. The parent directory is analogous to the x86 PAE PDPT, but there are 512 of them instead of just one, and each page directory is an entire page containing 512 entries instead of four. Like the PDPT, each parent directory enters the locations of second-level page directories, each of in turn contains the locations of the individual page tables. Finally, the page tables, each of which contains 512 page table entries, contain the physical locations of the pages in memory. All the "physical locations" in the preceding description are stored in these structures as PFNs.