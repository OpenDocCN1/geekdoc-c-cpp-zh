# PAGING: INTRODUCTION

```
// Extract the VPN from the virtual address
VPN = (VirtualAddress & VPN_MASK) >> SHIFT
```

```
// Form the address of the page-table entry (PTE)
PTEAddr = PTBR + (VPN + sizeof(PTE))
```

```
// Fetch the PTE
PTE = AccessMemory(PTEAddr)
```

```
// Check if process can access the page
if (PTE.Valid == False)
RaiseException(SEGMENTATION_FAULT)
elelse if (CanAccess(PTE.ProtectBits) == False)
RaiseException(PROTECTION_FAULT)
```

```
// Access is OK: form physical address and fetch it
offset = VirtualAddress & OFFSET_MASK
PhysAddr = (PTE.PFN << PFN_SHIFT) | offset
Register = AccessMemory(PhysAddr)
```

![](bbox=[0.258, 0.449, 0.693, 0.467])

Extra memory references are costly, and in this case will slow down the process by a factor of two or more.

And now you can hopefully see that there are real problems that we must solve. Without careful design of both hardware and software, page tables will cause the system to run too slowly, as well as take up too much memory. While seemingly a great solution for our memory virtualization needs, these two crucial problems must first be overcome.

# 18.5 A Memory Trace

Before coding, we now trace through a simple memory access example to demonstrate all the result of the memory accesses that occur when using paging. The code snippet (in C, a file called array.c) that we are interested in is follows:

```
int array[1000];
...
for (i = 0; i < 1000; i++)
array[i] = 0;
```

We compile array.c and run it with the following commands:

```
prompt gcc -o array array.c -Wall -O
prompt ./array
```