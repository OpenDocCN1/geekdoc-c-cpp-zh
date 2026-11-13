# 11.1 An Unrelated Puzzle

Consider the following puzzle: Two kittens are placed on opposite ends of a football field, 100 yards apart. They walk toward each other at the speed of 10 yards per minute. At the same time, their mother is at one end of the field. She can run at 100 yards per minute. The mother runs from one kitten to the other, making turns with no loss of speed, until the kittens (and thus the mother) meet at midfield. How far does the mother run?

It is not hard to solve this puzzle with a brute-force calculation. We leave the details to you, but one expects that this calculation will involve computing the sum of an infinite geometric series. Although this straightforward calculation will lead to an answer, it turns out that a much simpler solution can be arrived at by introducing an extra variable, namely, time.

Because the kittens are 100 yards apart and approach each other at a combined velocity of 20 yards per minute, it takes them five minutes to get to midfield. Since the mother runs 100 yards per minute, her total is 500 yards.

This puzzle illustrates the point that sometimes it is easier to solve a problem indirectly than directly. The amortized analyses that we perform will use this idea. We will introduce an extra variable, known as the **potential**, to allow us to prove results that seem very difficult to establish otherwise.

# 11.2 Binomial Queues

The first data structure we will look at is the binomial queue of Chapter 6, which we now review briefly. Recall that a binomial tree $B_0$ is a one-node tree, and for $k > 0$, the binomial tree $B_k$ is built by melding two binomial trees $B_{k-1}$ together. Binomial trees $B_0$ through $B_4$ are shown in Figure 11.1.

The rank of a node in a binomial tree is equal to the number of children; in particular, the rank of the root of $B_k$ is $k$. A binomial queue is a collection of heap-ordered binomial trees in which there can be at most one binomial tree $B_k$ for any $k$. Two binomial queues, $H_1$ and $H_2$, are shown in Figure 11.2.

The most important operation is **merge**. To merge two binomial queues, an operation similar to addition of binary integers is performed. At any stage we may have zero, one, two, or possibly three $B_k$ trees, depending on whether or not the two priority queues contain a $B_k$ tree and whether or not a $B_k$ tree is carried over from the previous step. If there is zero or one $B_k$ tree, it is placed as a tree in the resultant binomial queue. If there are two $B_k$ trees, they are melded into a $B_{k+1}$ tree and carried over; if there are three $B_k$ trees, one is placed as a tree in the binomial queue and the other two are melded and carried over. The result of merging $H_1$ and $H_2$ is shown in Figure 11.3.

Insertion is performed by creating a one-node binomial queue and performing a **merge**. The time to do this is $M + 1$, where $M$ represents the smallest type of binomial tree $B_M$ but not present in the binomial queue. Thus, insertion into a binomial queue that has a $B_0$ tree but no $B_1$ tree requires two steps. Deletion of the minimum is accomplished by removing the