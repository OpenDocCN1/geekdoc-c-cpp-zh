# EXAMPLE 15-3: TOWER OF HANOI

In the nineteenth century, a game called the Tower of Hanoi became popular in Europe. This game represents work that is under way in the temple of Brahma. At the creation of the universe, priests in the temple of Brahma were supposedly given three diamond needles, with one needle containing 64 golden disks. Each golden disk is slightly smaller than the disk below it. The priests' task is to move all 64 disks from the first needle to the third needle. The rules for moving the disks are as follows:

+   1. Only one disk can be moved at a time.
+   2. The removed disk must be placed on one of the needles.
+   3. A larger disk cannot be placed on top of a smaller disk.

The priests were told that once they had moved all of the disks from the first needle to the third needle, the universe would come to an end.

Our objective is to write a program that prints the sequence of moves needed to transfer the disks from the first needle to the third needle. Figure 15-6 shows the Tower of Hanoi problem with three disks.

![](bbox=[0.362, 0.489, 0.681, 0.596])

**FIGURE 15-6** Tower of Hanoi problem with three disks

As before, we think in terms of recursion. Let us first consider the case in which the first needle contains only one disk. In this case, the disk can be moved directly from needle 1 to needle 3. So let us consider the case in which the first needle contains only two disks. In this case, first we move the first disk from needle 1 to needle 2, and then we move the second disk from needle 1 to needle 3. Finally, we move the first disk from needle 2 to needle 3. Next, we consider the case in which the first needle contains three disks and then generalize this to the case of 64 disks (in fact, to an arbitrary number of disks).

Suppose that needle 1 contains three disks. To move disk number 3 to needle 3, the top two disks must first be moved to needle 2. Disk number 3 can then be moved from needle 1 to needle 3. To move the top two disks from needle 2 to needle 3, we use the same strategy as before. This time, we use needle 1 as the intermediate needle. Figure 15-7 shows a solution to the Tower of Hanoi problem with three disks.