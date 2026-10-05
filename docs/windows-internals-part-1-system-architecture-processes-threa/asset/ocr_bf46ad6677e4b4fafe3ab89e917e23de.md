# EXPERIMENT: Viewing PFN entries

You can examine individual PFN entries with the kernel debugger !pfn command. You need to supply the PFN as an argument. (For example, !pfn 0 shows the first entry, !pfn 1 shows the second, and so on.) In the following example, the PFN for virtual address 0xD20000 is displayed, followed by the PFN that contains the page directory, and then the actual:

```
1kd> !pte d20000

PDE at C0600030 PTE at C0600690
contains 00000003E989867 contains 8000000093257847
pfn 3e989 --DA--UVE pfn 3e9257 ---D---UW-W
```

You can use the Meminfo tool to obtain information about a PFN. Meminfo times you get more information than the debugger's output, and it does not require being booted into debugging mode. Here MemInfo's output for two PFNs:

```
C:\Tools\MemInfo.exe -p 3e989
0x3E989000 Page Table 5 N/A 0xC0006000 0x8E49940
C:\Tools\MemInfo.exe -p 3e9257
0x93257000 Process Private 5 windbg.exe 0x0D20000 N//
```

From left to right, the information shows the physical address, type, page priority, process name, virtual address, and potential extra information. Meminfo correctly recognized that the first PFN was a page table and the second PFN belongs to WinDbg, which was the active process when the !pte d20000 command was used in the debugger.

# Page file reclamation

We have already seen some mechanisms used by the memory manager to attempt to reduce memory consumption and thus reduce accessing pages. Using the standby and modified list is one such mechanism, and so is memory compression (see the "Memory compression" section later in this chapter). Another optimization the memory uses is directly related to accessing pages themselves.

CHAPTER 5 Memory management 444