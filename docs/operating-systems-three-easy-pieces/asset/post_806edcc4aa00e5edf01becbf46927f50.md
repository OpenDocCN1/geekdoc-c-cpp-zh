
# REDUNDANT ARRAYS OF INEXPENSIVE DISKS (RAIDS)

# ASIDE: THE RAID CONSISTENT-UPDATE PROBLEM

Before analyzing RAID-1, let us discuss a problem that arises in any multi-disk RAID system, known as the consistent-update problem [DAA05]. The problem occurs on a write to any RAID that has to update-multiple disks during a single costly operation. In this case, let us assume we are considering a mirrored disk array.

Imagine the issue is written to the RAID, and the RAID decides that it must be written to two disks, disk 0 and disk 1. The RAID issues the write to disk 0, but just before the RAID can issue the request to disk 1, a power loss (or system crash) occurs. In this unfortunate case, let us assume that the request to disk 0 completed (but clearly the request to disk 1 did not, as it was never issued).

The result of untimely power loss is that two copies of the block are now inconsistent; the copy on disk 0 is the new version, and the copy on disk 1 is the old. What we would like to happen is for the state of both disks to change atomically, i.e., either both should end up as the new version or neither.

The general way to solve this problem is to use a write-ahead log of some to first record what the RAID is about to do (i.e., update disks with a certain piece of data) before doing it. By this approach, we can ensure in the presence of a crash, the right thing will happen; by using a recovery procedure that repeats all pending transactions to the RAID, we can ensure that no two mirrored copies (in the RAID-1 case) are out of sync.

One note: because logging to disk on every write is prohibitively expensive, most RAID hardware includes a small amount of non-volatile RAM (e.g., battery-backed) where it performs this type of logging. Thus, consistent update is provided without the cost of logging to disk.

To analyze steady-state throughput, let us start with the sequential workload. When writing out disk sequentially, each logical write will result in two physical writes; for example, when we write logical block 0 (in the figure), the RAID internally would write it to both disk 0 and disk 1. Thus, we conclude that the maximum bandwidth during sequential writing to a mirrored array is $S/2$, or half the peak bandwidth.

Unfortunately, one might think the exact same performance during a sequential read could do better, because it only needs to read one copy of the data, not both. However, let's use an example to illustrate why this doesn't help much. Imagine we need to read blocks 0, 1, 2, 3, 4, 5, 6, and 7. Let's say we issue the read of 0 to disk 0, the read of 1 to disk 2, the read of 2 to disk 1, and the read of 3 to disk 3. We continue by issuing to 4, 5, 6, and 7 disks 0, 2, 1, and 3, respectively. One might naively think that because we are utilizing all disks, that we are achieving the full bandwidth of the array.

# REDUNDANT ARRAYS OF INEXPENSIVE DISKS (RaIDs)

To see that this is not (necessarily) the case, however consider the requests a single disk receives (say disk 0). First, it gets a request for block 0; then, it gets a request for block 4 (skipping block 2). In fact, each disk receives a request for every other block. While it is rotating over the skipped block, it is not delivering useful bandwidth to the client. Thus, each disk will only deliver half its peak bandwidth. And thus, the sequential read will only obtain a bandwidth of $(\frac{1}{2} \cdot S)$ MB/s.

Random reads are the best case for mirrored RAID. In this, we can distribute the reads across all the disks, and obtain the full possible bandwidth. Thus, for random reads, RAID-1 delivers $N \cdot R$ MB/s.

Finally, random writes perform as you might expect: $\frac{1}{2} \cdot R$ MB/s. Each logical write must turn into two physical, and while all the disks will be in use, the client will only receive half the bandwidth. Even though a write to logical block $x$ enters into two parallel writes to two physical disks, the bandwidth of many requests only achieves half of what we saw with striping. As we will soon see, getting the available bandwidth is actually pretty good!

# 3.6 RAID Level 4: Saving Space With Parity

We present a different method of adding redundancy to a disk array using *parity*. Parity-based approaches attempt to use less capacity and overcome the huge space penalty paid by mirrored systems. They do at a cost, however:

| Disk 0 | Disk 1 | Disk 2 | Disk 3 | Disk 4 |
| :--- | :--- | :--- | :--- | :--- |
| 0 | 1 | 2 | 3 | P0 |
| 4 | 5 | 6 | 7 | P1 |
| 8 | 9 | 10 | 11 | P2 |
| 12 | 13 | 14 | 15 | P3 |

**Figure 38:4: RAID-4 With Parity**

Here is an example five-disk RAID-4 system. For each stripe of data, we added a *parity* block that stores the redundant information for that stripe of blocks. For example, parity block P1 has redundant information that it calculated from blocks 4, 5, 6, and 7.

To compute parity, we need to use a mathematical function that allows us to write without the loss of any block from our stripe. It turns the simple function $XOR$ does the trick quite nicely. For a given set of bits, the XOR of all returns a 0 if there are an even number of 1s in the bits, and a 1 if there is an odd number of 1s. For example:

| C0 | C1 | C2 | C3 | P |
| :--- | :--- | :--- | :--- | :--- |
| 0 | 0 | 1 | 1 | XOR(0,0,1,1) = 0 |
| 0 | 1 | 0 | 0 | XOR(0,1,0,0) = 1 |

OPERATING SYSTEMS
[Version 1.01]

WWW.OSTEP.ORG

# REDUNDANT ARRAYS OF INEXPENSIVE DISKS (RAIDS)

In the first row (0,0,1,1), there are two 1s (C2, C3), and thus XOR of all of those values will be 0 (P); similarly, in the second row there is only one one (C1), and thus XOR will be 1 (P). You can remember this in a simple way: the number of 1s in any row, including the parity, must be an even (not odd) number; that is the invariant and the RAID must maintain in order for parity to be correct.

From the example above, you might also be able to guess how parity information can be used to recover from a failure. Imagine the column C2 is lost. To figure out what values must have in the column, we simply have to read the XOR parity bit and reconstruct the right answer. Specifically, assume the first row's value in column C2 is lost (it is a 1); by reading the other values in that row (0 from C0, 1 from C1, from C3 and 0 from the parity column P), we get the values 0, 1, and 0 because we know that XOR gives the number of 1s in each row and we know what the missing data must be: a 1. And how reconstruction works in a RAID-based scheme! Note also how we computed the reconstructed value: we just XOR the data bits and parity bits.
