# Sorting Data in an External File 641

each segment and select the record with the smaller sort key. If the record from $S_i$ is selected, the next step is to compare the second record of $S_i$ to the first record of $S_j$. This process continues until all of the records have been considered. The key observation is that at any step, the merge needs to look beyond the *leading edge* of each segment.

This observation may require a merge sort appropriate for the problem of sorting external files, if you modify the algorithm appropriately. Suppose that the 1,600 records are to be sorted in the file $F$ and you are not permitted to access this file. You will two work files, $F_1$ and $F_2$. One of the files will contain sorted records when the algorithm terminates. The algorithm has two phases: Phase 1 sorts each block of records, and Phase 2 performs a series of merges.

**Phase 1.** Read a block from $F$ into internal memory, sort its records using an internal sort, and write the sorted block out to $F_1$; before you read the next block of $F$. After you process 16 blocks of $F$, 16 sorted runs $R_1, ..., R_{16}$ are so in $F_1$; that is, $F_1$ contains 16 blocks of records, with the records sorted among themselves, as Figure 21-3a illustrates.
**Phase 2.** Is a sequence of merge steps. Each merge step merges pairs of sorted runs to form larger sorted runs, until the total number of sorted runs is halved. as Figure 21-3b shows, the first

![](bbox=[0.798, 0.245, 0.938, 0.258])

# **FIGURE 21-3**

+   (a) Sixteen sorted runs, one block each, in file $F_1$; (b) Eight sorted runs, two blocks each, in file $F_2$; (c) Four sorted runs, four blocks each, in file $F_3$; (d) Two sorted runs, eight blocks each, in file $F_2$

![](bbox=[0.062, 0.466, 0.768, 0.558])

![](bbox=[0.062, 0.577, 0.768, 0.672])

![](bbox=[0.062, 0.703, 0.768, 0.781])

![](bbox=[0.062, 0.811, 0.768, 0.893])