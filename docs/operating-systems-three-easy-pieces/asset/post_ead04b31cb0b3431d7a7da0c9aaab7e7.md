
# FLASH-BASED SSDs

The problem we have now should be obvious: physical pages 0 and 1, also marked VALID, have garbage in them, i.e., the old versions of blocks 100 and 101. Because of the log-structured nature of the device, overwrites create garbage blocks, which the device must reclaim to provide free space for new writes to take place.

The process of finding garbage blocks (also called dead blocks) and reclaiming them for use is garbage collection, and it is an important component of any modern SSD. The basic process is simple: find a block that contains one or more garbage pages, read in the live (non-garbage) pages from that block, write out those pages to the log, and (finally) reclaim the entire block for use.

Let's now illustrate with an example. The device decides it wants to reclaim any dead pages above. Block 0 has two dead pages (0 and 1) and two live blocks (pages 2 and 3, which contain blocks 2000 and 2001, respectively). To do so, the device:

- Read live data (pages 2 and 3) from block 0
- Write live data to end of the log
- Erase block (freeing it for later usage)

For the garbage collector to function, there must be enough information within each block to enable the SSD to determine whether each page is live or dead. One natural way to achieve this is to store, at some location within block, information about which logical blocks are stored within each page. The device can use the mapping table to determine whether page within the block holds live data or not.

From our example (before the garbage collection has taken place), block 0 held logical blocks 100, 101, 2000, 2001. By checking the mapping table (which, before garbage collection, contained 100->4, 101->5, 2000->2, 2001->3), the device can readily determine whether each of the pages within the SSD block holds live information. For example, 2000 and 2001 are live, 100 and 101 are not and are candidates for garbage collection.

When this garbage collection process is complete in our example, the state of the device is:

| | 100→4 | 101→5 | 2001→7 | Memory |
|---|---|---|---|---|
| Block: | 0 | 1 | 2 | |
| Page: | 00 01 02 03 04 05 06 07 08 09 10 11 | Flash Chip |
| Content: | | c1 c2 b1 b2 | | |
| State: | E E E E V V V V I I I | | |

As you see, garbage collection can be expensive, requiring reading and rewriting of live data. The ideal candidate for reclamation is a block that consists of only dead pages; in this case, the block can immediately be erased and used for new data, without expensive data migration.

© 2008– ARPACI-DSEAU
THREE
ASY PIECES

# ASIDE: A New Storage API Known As TRIM

When we think of hard drives, we usually just think of the most basic interface to read and write them: read and write (there is also some kind of cache flush command, ensuring that drives have alike persisted, but sometimes we omit it (for simplicity)). log-structured SSDs, and indeed, any device that has a flexible and changing mapping of logical-to-physical blocks, a new interface is useful, known as the trim operation.

The trim operation takes as address (and possibly a length) and simply informs the device that the block(s) by the address (and length) have been deleted; the device has no longer to track any information about the given address range. For a standard hard drive, trim isn't particularly useful, because the device has a static mapping of block addresses to platter, track, and sector(s). For a log-structured SSD, however, it is highly useful to know that a block is no longer needed, and the SSD can then remove this information from the FTL and reclaim the physical space during garbage collection.

Although we sometimes think of interface and implementation as separate entities, in this case, we see that the implementation shapes the interface. With complex mappings, knowledge of blocks are no longer needed for a more effective implementation.

To reduce GC costs, some SSDs overprovision the device [A+08]; by adding extra flash capacity, cleaning can be delayed and pushed to the background, performs done at one time when the device is less busy. Adding more capacity also increases internal bandwidth, which can be used for cleaning and thus not harm bandwidth to the client. Many modern drives overprovision in this manner, one key to achieving excellent performance.

# 44.9 Mapping Table Size

The second cost of log-structuring is the potential for extremely large mapping tables, with one entry for each 4-KB page of the device. With a large 1-TB SSD, for example, a single 4-byte entry per 4-KB page results in 1 GB of memory needed the device, just for these mappings! Thus, page-level FTL scheme is impractical.

# Block-Based Mapping

One approach to reduce the costs of mapping is to only keep a pointer per block of the device, reducing the amount of mapping information by a factor of page size. This block-level FTL is akin to having bigger page sizes in a virtual memory system; in that case, you use fewer bits for the VPN and have a larger offset in each virtual address.

Unfortunately, using a block-based mapping inside a log-based FTL does not work well for performance reasons. The biggest problem arises when a “small write” occurs (i.e., one that is less than the size of a physical block). In this case, the FTL must read a large amount of data from the old copy and copy it into a new one (along with the data from the small write). This data copying increases amplification greatly thus decreases performance.

To make this issue more clear, let’s look at an example. Assume the client previously wrote blocks 2000, 2001, 2003 (with contents, a, b, c, d), and that they are located within physical block 1 at physical pages 4, 5, 6, and 7. With per-page mappings, the translation would have to record mappings for these logical blocks: 2000–4, 2001–5, 2002–6, and 2003–7.

If we read, using block-mapping, the FTL only needs to record a single translation for all of this data. The address mapping, however, is slightly different than our previous examples. Specifically, if the logical address of the device is being chopped into chunks that are the size of the physical blocks within the flash, the logical block consists of two portions: a chunk number and an offset. Because we are assuming four blocks fit within each physical block, the offset portion of the logical addresses is 2 bits; the remaining (most significant) bits form the chunk number.

Logical blocks 2000, 2001, 2002 and 2003 all have the same chunk number (500), and have different offsets (0, 1, 2, and 3, respectively). Thus, with a block-level mapping, the FTL records that chunk 500 maps to block 1 (starting at physical page 4), as shown in this diagram:

Table: 500 → Memory

| Block | | 1 | 2 |
|---|---|---|---|
| Page | 00 01 02 03 04 05 06 07 08 09 10 11 | Flash Chip |
| Content: | | c1 c2 b1 b2 | | |
| State: | E E E E V V V V I I I | | |

As you see, garbage collection can be expensive, requiring reading and rewriting of live data. The ideal candidate for reclamation is a block that consists of only dead pages; in this case, the block can immediately be erased and used for new data, without expensive data migration.

© 2008– ARPACI-DSEAU
THREE
ASY PIECES

# FLASH-SSDs

# 601

| Block | | 1 | 2 |
|---|---|---|---|
| Page | 00 01 02 03 04 05 06 07 08 09 10 11 | Flash Chip |
| Content: | | c1 c2 b1 b2 | | |
| State: | E E E E V V V V I I I | | |

As you see, garbage collection can be expensive, requiring reading and rewriting of live data. The ideal candidate for reclamation is a block that consists of only dead pages; in this case, the block can immediately be erased and used for new data, without expensive data migration.

© 2008– ARPACI-DSEAU
THREE
ASY PIECES

# ASIDE: A New Storage API Known As TRIM

When we think of hard drives, we usually just think of the most basic interface to read and write them: read and write (there is also some kind of cache flush command, ensuring that drives have alike persisted, but sometimes we omit it (for simplicity)). log-structured SSDs, and indeed, any device that has a flexible and changing mapping of logical-to-physical blocks, a new interface is useful, known as the trim operation.

The trim operation takes as address (and possibly a length) and simply informs the device that the block(s) by the address (and length) have been deleted; the device has no longer to track any information about the given address range. For a standard hard drive, trim isn't particularly useful, because the device has a static mapping of block addresses to platter, track, and sector(s). For a log-structured SSD, however, it is highly useful to know that a block is no longer needed, and the SSD can then remove this information from the FTL and reclaim the physical space during garbage collection.

Although we sometimes think of interface and implementation as separate entities, in this case, we see that the implementation shapes the interface. With complex mappings, knowledge of blocks are no longer needed for a more effective implementation.

To reduce GC costs, some SSDs overprovision the device [A+08]; by adding extra flash capacity, cleaning can be delayed and pushed to the background, performs done at one time when the device is less busy. Adding more capacity also increases internal bandwidth, which can be used for cleaning and thus not harm bandwidth to the client. Many modern drives overprovision in this manner, one key to achieving excellent performance.

# 44.9 Mapping Table Size

The second cost of log-structuring is the potential for extremely large mapping tables, with one entry for each 4-KB page of the device. With a large 1-TB SSD, for example, a single 4-byte entry per 4-KB page results in 1 GB of memory needed the device, just for these mappings! Thus, page-level FTL scheme is impractical.

# Block-Based Mapping

One approach to reduce the costs of mapping is to only keep a pointer per block of the device, reducing the amount of mapping information by a factor of page size. This block-level FTL is akin to having bigger page sizes in a virtual memory system; in that case, you use fewer bits for the VPN and have a larger offset in each virtual address.

Unfortunately, using a block-based mapping inside a log-based FTL does not work well for performance reasons. The biggest problem arises when a “small write” occurs (i.e., one that is less than the size of a physical block). In this case, the FTL must read a large amount of data from the old copy and copy it into a new one (along with the data from the small write). This data copying increases amplification greatly thus decreases performance.

To make this issue more clear, let’s look at an example. Assume the client previously wrote blocks 2000, 2001, 2003 (with contents, a, b, c, d), and that they are located within physical block 1 at physical pages 4, 5, 6, and 7. With per-page mappings, the translation would have to record mappings for these logical blocks: 2000–4, 2001–5, 2002–6, and 2003–7.

If we read, using block-mapping, the FTL only needs to record a single translation for all of this data. The address mapping, however, is slightly different than our previous examples. Specifically, if the logical address of the device is being chopped into chunks that are the size of the physical blocks within the flash, the logical block consists of two portions: a chunk number and an offset. Because we are assuming four blocks fit within each physical block, the offset portion of the logical addresses is 2 bits; the remaining (most significant) bits form the chunk number.

Logical blocks 2000, 2001, 2002 and 2003 all have the same chunk number (500), and have different offsets (0, 1, 2, and 3, respectively). Thus, with a block-level mapping, the FTL records that chunk 500 maps to block 1 (starting at physical page 4), as shown in this diagram:

Table: 500 → Memory

| Block | | 1 | 2 |
|---|---|---|---|
| Page | 00 01 02 03 04 05 06 07 08 09 10 11 | Flash Chip |
| Content: | | c1 c2 b1 b2 | | |
| State: | E E E E V V V V I I I | | |

As you see, garbage collection can be expensive, requiring reading and rewriting of live data. The ideal candidate for reclamation is a block that consists of only dead pages; in this case, the block can immediately be erased and used for new data, without expensive data migration.

© 2008– ARPACI-DSEAU
THREE
ASY PIECES

# Hybrid Mapping

To enable writing but also reduce costs, many modern FTLs employ a **hybrid mapping** technique. With this approach, the FTL keeps a few blocks erased and directs all writes to them; these are called **log blocks**. Because the FTL wants to be able to write any page to any location within the log block without all the copying required by a block-based mapping, it keeps mappings for these log blocks.

The FTL logically has two types of mapping table in its memory: a small set of per-page mappings in what we call the log table, and a larger set of per-page mappings in the data table. When looking for a particular logical block, the FTL will consult the log table; if the logical block is not found, the FTL will consult the data table to find its location and access the requested.

The key to the hybrid mapping strategy is keeping the number of blocks small. To keep the number of log blocks small, the FTL has to periodically examine log blocks (which have a pointer per page) and switch them into blocks that can be pointed to by only a single block pointer. This switch is accomplished by one of three main techniques, based on the contents of the block [KK+02].

For example, say the FTL had previously written out log pages 1000, 1001, 1002, and 1003, and placed them in physical block 2 (physical OPERATING
SYSTEMS
[Version 1.01]

WWW.OSTEP.ORG
