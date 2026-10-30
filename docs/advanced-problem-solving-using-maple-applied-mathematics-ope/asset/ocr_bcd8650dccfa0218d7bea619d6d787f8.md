![](bbox=[0.196, 0.092, 0.805, 0.271])

Figure 2.2: Tower of Hanoi Puzzle¹

The game consists of moving this, by threading the disks on another peg, and by moving only one disk at a time, obeying the following rules:

+   I. After each move, the disks will all be stacked on one, two, or three pegs, in decreasing order from the base to the top.
+   
+   II. The top disk may be lifted from one of the three stacks of disks, and placed on a peg that is empty.
+   
+   III. The top disk may be lifted from one of the three stacks and placed on top of another stack, provided that the top disk on that stack is larger.

Lucas’ original La Tour d’Hanoi game had eight disks. The puzzle was a model to illustrate moving the legendary “Sacred Tower of Brahma,” which actually had “sixty-four levels in fine gold, trimmed with diamonds.” This tower was attended by monks of the Temple of Bernares who moved one disk a minute according to the long-established ritual that no larger disk could be placed on a smaller disk. The monks believed, so Lucas’s story went, that as soon as all sixty-four disks were transferred, the earth would collapse in a cloud of dust.

This legend is somewhat alarming, so let’s use induction to find a formula for the number of moves required to transfer n disks from the first peg to the third peg. Suppose that we have n + 1 disks. Then we can move n smaller disks from the first peg to the second peg in a(n) moves, the number of moves for n disks. Then we move the largest disk from the first peg to the third peg. Finally we move the n smaller disks from the second peg to the third peg in a(n) moves. Therefore, a(n+1) = a(n)+1+a(n) = 2a(n)+1. So the recursion relation that gives the number of moves required is a(n + 1) = 2a(n) + 1; the initial value is a(1) = 1, meaning that we start with the case where there is only one disk to move. Figure 2.3 shows a plausible flow diagram for the Tower of Hanoi.