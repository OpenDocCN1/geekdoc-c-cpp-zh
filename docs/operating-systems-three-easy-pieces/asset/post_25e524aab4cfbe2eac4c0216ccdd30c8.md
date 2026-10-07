
# PAGING: FASTER TRANSLATIONS (TLBs) 217

TIP: CACHING WHEN POSSIBLE
Caching is one of the most fundamental performance techniques in computer systems, one that is used again and again to make the “common-case fast” [HP06]. The idea behind hardware caches is to take advantage of locality: temporal locality in instruction and data references. There are usually two types of locality. With temporal locality, the idea is that an instruction or item that has been recently accessed will likely be re-accessed soon in the future. Think of variables or instructions in a loop; they are accessed repeatedly over time. With spatial locality, the idea is that if a program accesses memory at x, it will likely access memory near x. Imagine here searching through an array of some kind, accessing one element and then the next. Of course, these properties depend on the exact nature of the program, and thus are not hard-and-fast but more rules of thumb.

Hardware caches, for instructions, data, or other translations (in our TLB) take advantage of locality by keeping copies of memory in fast, on-chip memory. Instead of having to go to a (slow) memory in a cache; if it does, the processor can check if a nearby copy exists quickly (i.e., in a few CPU cycles) and avoid spending the costly time to access memory (nanoseconds).

You might be wondering: if caches (like the TLB) are so great, why do we just make bigger caches and keep all of data in them? Unfortunately, here we run into more fundamental laws like those of physics. If you want a fast cache, it has to be small, as issues like speed of light and other physical constraints become relevant. Any large cache by definition is slow, and thus defeats the purpose. Thus, we are stuck with small, fast caches; the question that remains is how to use them to improve performance.

If the array had simply been twice as big (32 bytes, not 16), the array would suffer even fewer misses. As typical page sizes are more like 4KB, the types of dense, array-based accesses achieve excellent TLB performance, encountering only a single miss per page of accesses.

One last point about TLB performance: if the program, after this loop completes, accesses the array again, we'd likely see an even better result, assuming we have a big TLB to cache the needed translations: hit, hit, hit, hit, hit... In this case, the TLB hit rate would be high because of temporal locality, i.e., the quick-referencing of memory items in time. Like any cache, TLBs rely upon both spatial and temporal locality for success, which are proper properties. If the program of interest exhibits such locality (and many programs do), the TLB hit rate will likely be high.

© 2008–19, ARPACI-DUSSEAU

THREE EASY PIECES

# 218 PAGING: FASTER TRANSLATIONS (TLBs)

```c
VPN = (VirtualAddress & VPN_MASK) >> SHIFT
(Success, TlbEntry) // TLB_Lookup (VPN)
if (Success == True) // TLB Hit
    if (CanAccessTlbEntry.ProtectBits) == True)
        Offset = VirtualAddress & OFFSET_MASK
        PhysAddr = (TlbEntry.PFN << SHIFT) | Offset
        Register = AccessMemory(PhysAddr)
    else
        RaiseException (PROTECTION_FAULT)
else // TLB Miss
    RaiseException (TLB_MISS)
```

Figure 19.3: TLB Control Flow Algorithm (OS Handled)

# 19.3 Who Handles The TLB Miss?

More architectures (a couple of, MIPS R10k [H93] or Sun's SPARC v9 [WG00], RISC or reduced-instruction system computers) have a *software-managed TLB*. On a TLB miss, the hardware raises an exception (in Line 11 in Figure 19.3), which pauses the current instruction stream, changes the privilege level to kernel mode, and jumps to a *trap handler*. As you might guess, this trap handler is code within the OS that is written with the express purpose of handling TLB misses. When run, the code will lookup the translation in the page table, use "privileged" instructions to update the TLB, and return from the trap; at this point, the hardware retrieves the instruction (resulting in a TLB hit).

Let's discuss a couple of important details. First, the return-from-trap instruction needs to be a little different from the return-from-trap used before servicing a system call. In the case, the return-from-trap should resume execution at the instruction *after* the trap into the OS, just as from a procedure call returns to the instruction immediately calling into the procedure. In the former case, returning from a TLB miss-handling trap, the hardware must resume execution at the instruction that *caused* the trap; this retry lets the in...

OPERATING SYSTEMS
[VERSION 1.01]
WWW.OSTEP.ORG

# PAGING: FASTER TRANSLATIONS (TLBs)

# ASIDE: RISC vs. CISC

In the 1980s, a great battle took place in the computer architecture community. On one side was the CISC camp, which stood for **Complex Instruction Set Computing**; on the other side was RISC, for **Reduced Instruction Set Computing [PS81]**. The RISC side was spear-headed by David Patterson at Berkeley and John Hennessy at Stanford (who are also co-authors of some famous papers [H86]), although later John Cocke was recognized with a Turing Award for...

The primary advantage of software-managed approach is flexibility: the OS can decide...

© 2008–19, ARPACI-DUSSEAU
THREE EASY PIECES

# 257
# PAGING: FASTER TRANSLATIONS (TLBs)

# ASIDE: TLB Valid Bit vs Page Table Bit ownA common mistake is to confuse the TLB with those in page table. In a page table, when a TLB entry is marked invalid, it means the page has not been allocated. The TLB valid bit, in contrast, simply refers to whether the entry has a valid translation. When system boots, for example, a common initial state for each TLB entry is to set invalid, because... Once programs start running and accessing their address spaces, the TLB is slowly populated. The TLB valid bit is quite useful when performing a context switch, as we will discuss further. By setting all TLB entries to invalid, the system can ensure that about-to-run process does not accidentally use... from a previous process. The hardware doesn’t do much on a miss: just raise an exception and let the...

# 19.4 TLB Contents: What’s In There?

Let’s look at the contents of the TLB in more detail. A typical TLB might have 32, 64, or 128 entries and be what is called fully associative. Basically, this means that any given translation can be anywhere in the TLB, and that the hardware will search the entire TLB in parallel to find the desired translation.

| VPN | PFN | other bits |

Note that both VPN and PFN are present in each entry, as a translation could end up in any of these locations (hardware terms, the TLB is known as a fully-associative cache). The hardware searches the entries in parallel to see there is match.

More interesting are the “other bits”. For example, the TLB commonly has a valid bit, which says whether the entry has a valid translation or not. Also common are protection bits, which determine how a page can be accessed (as in the page table). For example, code pages might be marked read and execute, whereas heap pages might be marked read and write. There may also be a few other fields, including an address-space identifier, a dirty bit, and so forth; see below for more information.
