# FLASH-BASED SSDs

# ASIDE: KEY SSD TERMS

+   - A flash chip consists of many banks, each of which is organized into erase blocks (sometimes just called blocks). Each block is further subdivided into some number of pages.

+   - Blocks are large (128KB-2MB) and contain many pages, which are relatively small (1KB-8KB).

+   - To read from flash, issue a read command with an address and length; this allows a client to read one or more pages.

+   - Writing flash is more complex. First, the client must erase the entire block (which deletes all information within the block). Then, the client can program each page exactly once, thus completing the write.

+   - A new trim operation is useful to tell the device when a particular block (or range of blocks) is no longer needed.

+   - Flash reliability is mostly determined by wear out; if a block is erased and programmed too often, it will become unusable.

+   - A flash-based solid-state storage device (SSD) behaves as if were a normal block-based read/write disk; by using a flash translation layer (FTL), it transforms reads and writes from a client into reads, erases, and programs to underlying flash chips.

+   - Most FTLs are log-structured, which reduces the cost of writing by minimizing erase/program cycles. An in-memory translation layer tracks where logical writes were located within the physical medium.

+   - One key problem with log-structured FTLs is the cost of garbage collection, which leads to write amplification.

+   - Another problem is the size of the mapping table, which can become quite large. Using a hybrid mapping or caching pieces of the FTL are possible remedies.

+   - One last problem is wear leveling; the FTL must occasionally migrate data from blocks that are mostly read in order to ensure blocks also receive their share of the erase/program load.

OPERATING SYSTEMS
[Version 1.01]

WWW.OSTEP.ORG