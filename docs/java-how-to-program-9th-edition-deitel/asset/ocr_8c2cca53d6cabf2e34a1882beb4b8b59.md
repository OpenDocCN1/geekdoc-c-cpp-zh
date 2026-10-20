move a stack of golden disks from one diamond peg to another (Fig. 18.10). The initial stack has 64 disks threaded onto one peg and arranged from bottom to top by decreasing size. The priests are attempting to move the stack from one peg to another under the constraints that exactly one disk is moved at a time and at no time may a larger disk be placed above a smaller disk. Three pegs are provided, one being used for temporarily holding disks. Supposedly, the world will end when the priests complete their task, so there’s little incentive for us to facilitate their efforts.

![](bbox=[0.15, 0.26, 0.8, 0.5])

Fig. 18.10 | Towers of Hanoi for the case with four disks.

Let’s assume that the priests are attempting to move the disks from peg 1 to peg 3. We wish to develop an algorithm that prints the precise sequence of peg-to-peg disk transfers.

If we try to find an iterative solution, we’ll likely find ourselves hopelessly “knotted up” in managing the disks. Instead, attacking this problem recursively quickly yields a solution. Moving n disks can be viewed in terms of moving only n − 1 disks (hence the recursion) as follows:

+   1. Move n − 1 disks from peg 1 to peg 2, using peg 3 as a temporary holding area.
+   2. Move the last disk (the largest) from peg 1 to peg 3.
+   3. Move n − 1 disks from peg 2 to peg 3, using peg 1 as a temporary holding area.

The process ends when the last task involves moving n = 1 disk (i.e., the base case). This task is accomplished by moving the disk, without using a temporary holding area.

In Fig. 18.11, method solveTowers (lines 6–25) solves the Towers of Hanoi, given the total number of disks (in this case 3), the starting peg, the ending peg, and the temporary holding peg as parameters. The base case (lines 10–14) occurs when only one disk needs to be moved from the starting peg to the ending peg. In the recursion step (lines 18–24), line 18 moves disks - 1 disks from the first peg (sourcePeg) to the temporary holding peg (tempPeg). When all but one of the disks have been moved to the temporary peg, line 21 moves the largest disk from the start peg to the destination peg. Line 24 finishes the rest of the moves by calling the method solveTowers to recursively move disks - 1 disks from the temporary peg (tempPeg) to the destination peg (destinationPeg), this time using the first peg (sourcePeg) as the temporary peg. Line 35 in main calls the recursive solveTowers method, which outputs the steps to the command prompt.