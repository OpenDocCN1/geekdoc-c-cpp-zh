PAGING: SMALLER TABLES 239

# More Than Two Levels

In our example thus far, we've assumed that multi-level page tables only have two levels: a page directory and pieces of the page table. In some cases, a deeper tree is possible (and indeed, needed).

Let's take a simple example and use it to show how a multilevel table can be useful. In this example, assume we have a 30-bit virtual address space, and a 512 (byte) page size. Our virtual address has a 21-bit virtual page number and a 9-bit offset.

Remember our goal in constructing a multi-level page table: to make each piece of the page table fit within a single page. Thus, we've only considered the page table itself, however, if the page directory gets too big?

To determine how many levels are needed in a multi-level to make all pieces of the page table fit within a page, we start by determining how many page-table entries fit within a page. Given our page size of 512 bytes, and using a PTE size of 4 bytes, you should see that you can fit 128 PTES on a single page. When we index into a page of the page bits, we can conclude we need the least 7 bits (log2128) of the VPN as an index.

| VPN | offset |

| 29 | 28 | 27 | 26 | 25 | 24 | 23 | 22 | 21 | 20 | 19 | 18 | 17 | 16 | 15 | 14 | 13 | 12 | 11 | 10 | 9 | 8 | 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0 |

| Page Directory Index | Page Table Index |

You might also notice from the diagram above how many bits are left in the (large) page directory: 14. If our page directory has 2^14 entries, it spans not one 128, and thus our goal of making every piece of the multi-level page table fit into page vanishes.

To remedy this, we build a further level of the tree, by splitting the page directory into multiple pages, and adding another page directory on top of that, to point to the pages of the page directory. We can split our virtual address as:

| VPN | offset |

| 29 | 28 | 27 | 26 | 25 | 24 | 23 | 22 | 21 | 20 | 19 | 18 | 17 | 16 | 15 | 14 | 13 | 12 | 11 | 10 | 9 | 8 | 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0 |

| PD Index 0 | PD Index 1 | Page Table Index |

Now, when indexing the upper-level page directory, we use the top bits of the virtual address (PD Index 0 in the diagram); this index can be used to fetch the page-directory entry from the top-level page directory. If so, the second level of the page directory is consulted by combining the physical frame number from the top-level PDE and the

© 2008–19, ARPACI-DUSAU

THREE
EASY
PIECES