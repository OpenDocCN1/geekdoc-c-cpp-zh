# 44.7 A Log-Structured FTL

For these reasons, most FTLs log structured, an idea useful in both storage devices (as we'll see now) and file systems above them (as we'll see in the chapter on log-structured file systems). Upon a write to logical block N, the device appends the write to the new free spot in the currently-written-to-block; we call this style of writing logging. For simplicity, assume that for block N, the device keeps a mapping table (in its memory, and persistent, in some form, the device); this table stores the physical address of each logical block in the ssd.

Let's go through an example to make sure how the basic-based approach works. To the client, the device looks like a typical disk, which it can read and write 512-byte sectors (or groups of sectors). Assume that the SSD is reading or writing 4-KB sized chunks. Let us further assume that the SSD contains some large number of 16-KB blocks, each divided into four 4-KB pages; these parameters are unrealistic (flash blocks usually consist of many pages) but will serve our didactic purposes quite well.

Assume the client issues the following sequence of operations:

+   * Write(100) with contents a1
* Write(101) with contents a2
* Write(2000) with contents b1
* Write(2001) with contents b2

These logical blocks (e.g., 100) are used by the client of the SSD (e.g., a file system) to remember where information is located.
Internally, the device must transform these blocks into the erase and program operations supported by the hardware, and somehow record, for each logical block address, Assume that all blocks of the SSD are currently not valid, stores its data. and must be erased before any page can be programmed. Here we show the initial state of our SSD, with all pages marked INVALID (i):

| Block | 0 | | 2 |
|---|---|---||
| Page | 00 01 02 03 04 05 06 07 08 09 10 11 |
| Content | | | |
| State | i i i i i i i i i i i i i i i i |

When the first write is received by the SSD (to logical block 100), the FTL decides to write it to physical block 0, which contains four physical pages: 0, 1, 2, and 3. Because the block is not erased, we cannot write to it; the device must first issue an erase command to block 0. Doing so leads to the following state:

| Block | 0 | | 2 |
|---|---|---||
| Page | 00 01 02 03 04 05 06 07 08 09 10 11 |
| Content | | | |
| State | E E E E i i i i i i i i i i i |