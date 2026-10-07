PAGING: FASTER TRANSLATIONS (TLBs) 223

# 19.6 Issue: Replacement Policy

As with any cache, and also with the TLB, one more issue that we must consider is cache replacement. Specifically, when we are installing a new entry in the TLB, we have to replace an old one, and thus the question: which one to replace?

> THE CRUX: HOW TO DESIGN TLB REPLACEMENT POLICY
Which TLB entry should be replaced when we add a new TLB entry? The goal, of course, is to minimize the miss rate (or increase hit rate) and improve performance.

We will study policies in detail; here we tackle the problem of swapping pages; one common approach is to evict the least-recently-used or LRU entry. LRU tries to take advantage of locality in the memory-reference stream, assuming that it is an entry that has not been used is a good candidate for eviction. Another typical approach is to use a random policy, which evicts a TLB mapping at random. Such a policy is useful due to its simplicity and helps avoid corner-behaviors; for example, a “reasonable” policy as LRU behaves quite unreasonably when a program loops over n + 1 pages with a TLB of size n; in this case, LRU misses upon every entry, whereas random does much better.

# 19.7 A Real TLB

Finally, let's briefly look at a real TLB. This example is from the MIPS R4000 [1993], a modern system that uses software-managed TLBs; a simplified MIPS R4000 supports a 32-bit address space with 4KB pages. We would expect a 20-bit VPN and 12-bit offset in our typical virtual address. However, as we turn out, user addresses will only come from half the address space (the rest reserved for the kernel) and only 19 bits of VPN are needed. The VPN translates to a 24-bit physical frame number (PFN), and hence can support systems with up to 64GB (physical) memory (4KB pages).

There are a few interesting bits in the MIPS TLB. We see a global bit (G), which is used for pages that are globally-shared among processes. If the global bit is set, the ASID is ignored. We also see the 8-bit ASID, which the OS can use to distinguish between address spaces (as

| VPN | G | ASID |
|---|---|---|
| PFN | C | D |

Figure 19:4: A MIPS TLB Entry

© 2008–19, ARPACI-DUSSEAU

THREE
EASY
PECES