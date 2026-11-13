We can break this into three basic steps.

+   1. Move the disk 4 and the ones smaller than it that from the peg A (source) to peg C (spare), using peg B (dest) as a spare. We achieve it recursively using the same function. After finishing this, we will have all the disks smaller than disk 4 on peg C (Fig. 4.3).

![](bbox=[0.29, 0.21, 0.81, 0.34])

Fig. 4.3 Tower of Hanoi—step 1

+   2. Now, with all the smaller disks on the spare peg C, we can move disk 5 from peg A to peg B (Fig. 4.4).

![](bbox=[0.29, 0.45, 0.81, 0.59])

Fig. 4.4 Tower of Hanoi—step 2

+   3. Finally, we want disk 4 and the smaller disks to be moved from peg C to peg B. We do this recursively using the same function again. At the end, we have disk 5 and the smaller ones on peg B (Fig. 4.5).

![](bbox=[0.29, 0.72, 0.81, 0.86])

Fig. 4.5 Tower of Hanoi—final step