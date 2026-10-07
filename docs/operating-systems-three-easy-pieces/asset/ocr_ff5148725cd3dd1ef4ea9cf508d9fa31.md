# PAGING: INTRODUCTION

| page table: | page frame 0 of physical memory |
|---|---|
| 0 3 7 5 2 | |
| 16 (unused) | page frame 1 |
| 32 page 3 of AS | page frame 2 |
| 48 page 0 of AS | page frame 3 |
| 64 (unused) | page frame 4 |
| 80 page 2 of AS | page frame 5 |
| 96 (unused) | page frame 6 |
| 112 page 1 of AS | page frame 7 |
| 128 | |

Figure 18.4: Example: Page Table in Kernel Physical Memory

Note the offset stays the same (i.e., it is not translated), because the offset just tells us which byte within the page we want. Our final physical address is 1110101 (117 in decimal), and is exactly where we want our load to fetch data from Figure 18.2, page 198.

With this basic overview in mind, we can now ask (and hopefully, answer) a few basic questions you may have about paging. For example, where are these page tables stored? And how big are the tables? Does paging make the system (too slow)? These and other puzzling questions are answered, at least in part, in the text below. Read on!

# 18.2 Where Are Page Tables St?

Page tables can get terribly large, much bigger than the small segment address/base pairs we have discovered previously. For example, imagine a typical 32-bit address space, with 4KB pages. This virtual address splits into a 20-bit VPN and 12-bit offset (recall that 10 bits would be needed for a 1KB page size, and just two more to get to 4KB).

A 20-bit VPN implies that there are ²²⁰ translations that the OS would have to manage for each process (that's roughly a million); assuming we need 4 bytes per page entry (PTE) to hold the physical translation plus any other useful stuff, we get an immense 4MB of memory needed for each page table! That is pretty large. Now imagine there are 100 processes running; this means the OS would need 400MB of memory just for all those address translations! Even in the modern era, where

© 2008–19, ARPACI-DUSSE

THREE
ASY
PIECES