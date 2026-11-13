
![](img/e449061a0cac9cafaefd979fab665b33_533_0.png)

Figure 10.69 Two searches that arrive at identical position

tree is actually constructed by the algorithm. The game tree is just an abstract concept.) The value of the game tree is 44.

Figure 10.71 shows the evaluation of the same game tree with several (but not all possible) unevaluated nodes. Almost half of the terminal nodes have not been checked. We show that evaluating them would not change the value at the root.

First, consider node D. Figure 10.72 shows the information that has been gathered when it is time to evaluate D. At this point, we are still in findHumanMove and are contemplating a call to findCompMove on D. However, we already know that findHumanMove will return at most 40, since it is a min node. On the other hand, its max node parent has already found a sequence that guarantees 44. Nothing that D does can possibly increase this value. Therefore, D does not need to be evaluated. This pruning of the tree is known as α pruning. An identical situation occurs at node B. To implement α pruning, findCompMove passes its tentative maximum (α) to findHumanMove. If the tentative minimum of findHumanMove falls below this value, then findHumanMove returns immediately.

A similar thing happens at nodes A and C. This time, we are in the middle of a findCompMove and are about to make a call to findHumanMove to evaluate C. Figure 10.73 shows the situation that is encountered at node C. However, the findHumanMove, at the min

![](img/e449061a0cac9cafaefd979fab665b33_533_1.png)

Figure 10.70 A hypothetical game tree

![](img/e449061a0cac9cafaefd979fab665b33_534_0.png)

Figure 10.71 A pruned game tree

![](img/e449061a0cac9cafaefd979fab665b33_534_1.png)

Figure 10.72 The node marked ? is unimportant

![](img/e449061a0cac9cafaefd979fab665b33_534_2.png)

Figure 10.73 The node marked ? is unimportant

level, which has called findCompMove, has already determined that it can force a value of at most 44 (recall that low values are good for the human side). Since findCompMove has a tentative maximum of 68, nothing that C does will affect the result at the min level. Therefore, C should not be evaluated. This type of pruning is known as β pruning; it is the symmetric version of α pruning. When both techniques are combined, we have α-β pruning.

```
1 /**
2 * Same as before, but perform alpha-beta pruning.
3 * The main routine should make the call with
4 * alpha = COMP_LOSS and beta = COMP_WIN.
5 */
6 /* TicTacToe::findCompMove( int & bestMove, int alpha, int beta )
7 {
8 int i, responseValue;
9 int dc; // dc means don't care; its value is unused
10 int value;
11
12 if( fullBoard( ) )
13 value = DRAW;
14 else
15 if( immediateCompWin( bestMove ) )
16 return COMP_WIN; // bestMove will be set by immediateCompWin
17 else
18 {
19 value = alpha; bestMove = 1;
20 for( i = 1; i <= 9 && value < beta; ++i ) // Try each square
21 {
22 if( isEmpty( i ) )
23 {
24 place( i, COMP );
25 responseValue = findHumanMove( dc, value, beta );
26 unplace( i ); // Restore board
27
28 if( responseValue > value )
29 {
30 // Update best move
31 value = responseValue;
32 bestMove = i;
33 }
34 }
35 }
36 }
37 return value;
38 }
```

### Figure 10.74 Minimax tic-tac-toe algorithm with α-β pruning: computer selection

Implementing α-β pruning requires surprisingly little code. Figure 10.74 shows half of the α-β pruning scheme (minus type declarations); you should have no trouble coding the other half.

To take full advantage of α-β pruning, game programs usually try to apply the evaluation function to nonterminal nodes in an attempt to place the best moves early in the

search. The result is even more pruning than one would expect from a random ordering of the nodes. Other techniques, such as searching deeper in more active lines of play, are also employed.

In practice, α-β pruning limits the searching to only O(√N) nodes, where N is the size of the full game tree. This is a huge savings and means that searches using α-β pruning can go twice as deep as compared to an unpruned tree. Our tic-tac-toe example is not ideal, because there are so many identical values, but even so, the initial search of 97,162 nodes is reduced to 4,493 nodes. (These counts include nonterminal nodes.)

In many games, computers are among the best players in the world. The techniques used are very interesting, and can be applied to more serious problems. More details can be found in the references.

## Summary

This chapter illustrates five of the most common techniques found in algorithm design. When confronted with a problem, it is worthwhile to see if any of these methods apply. A proper choice of algorithm, combined with judicious use of data structures, can often lead quickly to efficient solutions.

## Exercises

- 10.1 Show that the greedy algorithm to minimize the mean completion time for multiprocessor job scheduling works.

- 10.2 The input is a set of jobs \(j_1, j_2, \dots, j_N\), each of which takes one time unit to complete. Each job \(j_i\) earns \(d_i\) dollars if it is completed by the time limit \(t_i\), but no money if completed after the time limit.
  - a. Give an \(O(N^2)\) greedy algorithm to solve the problem.
  - **b. Modify your algorithm to obtain an \(O(N \log N)\) time bound. (Hint: The time bound is due entirely to sorting the jobs by money. The rest of the algorithm can be implemented, using the disjoint set data structure, in \(O(N \log N)\).)**

- 10.3 A file contains only colons, spaces, newlines, commas, and digits in the following frequency: colon (100), space (605), newline (100), comma (705), 0 (431), 1 (242), 2 (176), 3 (59), 4 (185), 5 (250), 6 (174), 7 (199), 8 (205), 9 (217). Construct the Huffman code.

- 10.4 Part of the encoded file must be a header indicating the Huffman code. Give a method for constructing the header of size at most \(O(N)\) (in addition to the symbols), where \(N\) is the number of symbols.

- 10.5 Complete the proof that Huffman's algorithm generates an optimal prefix code.

- 10.6 Show that if the symbols are sorted by frequency, Huffman's algorithm can be implemented in linear time.

- 10.7 Write a program to implement file compression (and uncompression) using Huffman's algorithm.

- 10.8 Show that any online bin packing algorithm can be forced to use at least 3/2 the optimal number of bins, by considering the following sequence of items: N items of size 1/2 - epsilon, N items of size 1/4 + epsilon, N items of size 1/4 + epsilon.

- 10.9 Give a simple analysis to show the performance bound for first fit decreasing bin packing when
  - a. The smallest item size is larger than 1/3.
  - b. The smallest item size is larger than 1/4.
  - c. The smallest item size is smaller than 1/11.

- 10.10 Explain how to implement first fit and best fit in O(N log N) time.

- 10.11 Show the operation of all the bin packing strategies discussed in Section 10.1.3 on the input 0.42, 0.25, 0.27, 0.07, 0.72, 0.86, 0.09, 0.44, 0.50, 0.68, 0.73, 0.31, 0.78, 0.17, 0.79, 0.37, 0.73, 0.23, 0.30.

- 10.12 Write a program that compares the performance (both in time and number of bins used) of the various bin packing heuristics.

- 10.13 Prove Theorem 10.7.

- 10.14 Prove Theorem 10.8.

- 10.15 N points are placed in a unit square. Show that the distance between the closest pair is O(N^-1/2).

- 10.16 Argue that for the closest-points algorithm, the average number of points in the strip is O(sqrt(N)). (Hint: Use the result of the previous exercise.)

- 10.17 Write a program to implement the closest-pair algorithm.

- 10.18 What is the asymptotic running time of quickselect using a median-of-median-of-three partitioning strategy?

- 10.19 Show that quickselect with median-of-median-of-seven partitioning is linear. Why is median-of-median-of-seven partitioning not used in the proof?

- 10.20 Implement the quickselect algorithm in Chapter 7, quickselect using median-of-median-of-five partitioning, and the sampling algorithm at the end of Section 10.2.3. Compare the running times.

- 10.21 Much of the information used to compute the median-of-median-of-five is thrown away. Show how the number of comparisons can be reduced by more careful use of the information.

- 10.22 Complete the analysis of the sampling algorithm described at the end of Section 10.2.3, and explain how the values of delta and s are chosen.

- 10.23 Show how the recursive multiplication algorithm computes XY, where X = 1234 and Y = 4521. Include all recursive computations.

- 10.24 Show how to multiply two complex numbers X = a + bi and Y = c + di using only three multiplications.

- 10.25 a. Show that

  X_L Y_R + X_R Y_L = (X_L + X_R)(Y_L + Y_R) - X_L Y_L - X_R Y_R
