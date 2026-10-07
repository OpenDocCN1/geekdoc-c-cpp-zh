# REDUNDANT ARRAYS OF INEXPENSIVE DISKS (RAIDS)

> ASIDE: THE RAID MAPPING PROBLEM

Before studying the capacity, reliability, and performance characteristics of the RAID, we first present an analysis on what we call the **mapping problem**. This arises in all RAID arrays; simply put, given a logical block to read or write, how does the RAID know exactly which physical disk and offset to access?

For these simple RAID levels, we do not need much sophistication in order to correctly map logical blocks onto their physical locations. Take the first striped example (chunk size = 1 block = 4KB). In this case, given a logical block A, the RAID can easily compute the desired disk and offset with two equations:

```
Disk = A % number_of_disks
Offset = A / number_of_disks
```

Note that these equations work for a simple example (e.g., 4 / 3 = 1.33333...). Let's see how these equations work for a simple example. Imagine in the first RAID above that a request arrives for block 14. Given that there are 4 disks, would this mean that the disk we are interested in is (14 % 4 = 2)? The exact offset is calculated as (14 / 4 = 3). Thus, block 14 should be on the fourth block (block 3, starting at 0) of the third disk (block 2, starting at 0), which is exactly where it is. You can think about how these equations would be modified to support different chunk sizes. Try it! It's not too hard.

# Chunk Sizes

Chunk size mostly affects the performance of the array. For example, a small chunk size implies that many files will be striped across many disks, increasing the parallelism of reads and writes to a single file; however, the positioning time to access blocks across multiple disks increases, because the positioning time for the entire request is determined by the maximum of the positioning times across the requests all.

A big chunk size, on the other hand, reduces intra-file parallelism, and relies on multiple concurrent requests to achieve high throughput. However, large chunk sizes reduce positioning time; if, for example, a file fits within a chunk and is placed on a single disk, the positioning time incurred while accessing it will just be the positioning time of a single disk.

Thus, determining the "best" chunk size is hard to do, as it requires a great deal of knowledge about the workload presented to the disk system [CL95]. For the rest of this discussion, we will assume that the array uses a chunk size of a single block (4KB). Most arrays use larger chunk sizes (e.g., 64 KB), but for the issues we use a single block for the sake of simplicity.

© 2008–19, ARPAC-DUSSEAU

THREE
EASY
PIECES