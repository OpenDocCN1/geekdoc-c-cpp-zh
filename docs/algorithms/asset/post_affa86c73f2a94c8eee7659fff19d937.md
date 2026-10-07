
# Chapter 8

## Algorithms 25

A search problem is specified by an algorithm C that takes two inputs, an instance I and a proposed solution S, and runs in time polynomial in |I|. We say S is a solution to I if and only if C(I, S) = true.

Given the importance of the SAT search problem, researchers over the past 50 years have tried to find efficient ways to solve it, but without success. The fastest algorithms we have are still exponential over worst-case inputs.

Yet, there are two natural sets of SAT for which we have good algorithms. If all clauses contain at most one literal, the Boolean formula is a Horn formula, and a satisfying truth assignment, if one exists, can be found by the greedy algorithm of Section 5.3. Alternatively, if all have only two literals, then graph theory comes into play, and SAT can be solved in linear time by finding the strongly connected components of a particular graph constructed from the instance (recall Exercise 5.28). In fact, Chapter 9 will see a different polynomial algorithm for this special case, which is called 2SAT.

On the other hand, if we are just a little more permissive and allow clauses to contain three literals, the resulting problem, known as 3SAT (an example of which we saw earlier), once again becomes hard to solve!

## The traveling salesman problem

In the traveling salesman problem (TSP) we have n vertices 1...n and n(n−1)/2 distances between them, as well as a budget b. We are asked to find a tour, a cycle that passes through every vertex exactly once, of total cost b less to report that no such tour exists. That is, we seek a permutation τ(1)...τ(n) of the vertices such that they are toured in this order, the total cost covered is at most b:

$$d_{τ(1),τ(2)} + d_{τ(2),τ(3)} + \dots + d_{τ(n),τ(1)} \leq b. $$

See Figure 8.1 for an example (only some of the distances are shown); assume the rest are very large.

Notice how we have defined the TSP as a search problem: given an instance, a tour budget (or report that no tour exists). But why are we expressing the traveling salesman problem in this way, when in reality it is an optimization problem, in which the shortest possible tour is sought? Why do we dress it up as search?

For a good reason. Our plan in this chapter is to compare and relate. The framework of search problems is helpful in this regard, because it encompasses optimization problems like the TSP in addition to true search SAT.

Turning an optimization problem into a search problem does not change its difficulty at all, because the two versions reduce to one another. Any algorithm that solves the optimization TSP also solves the search problem: find the optimum tour and if it is within budget, return it; if not, there is no solution.

# Figure 8.1 The optimal traveling salesman tour, shown in bold, has length 18.

![](img/3dd1f1364df8f87b80683fc32a15b999_246_0.png)

Conversely, an algorithm for the search problem can also be used to solve the optimization problem. To see why, first suppose that we knew the cost of the optimum tour; then we could find this tour by calling the algorithm for the search problem, using the optimum cost as the budget. But, how do we know the optimum cost? Easy: By binary search (See Exercise 8.1.)

Incidentally, there is a subtlety: Why do we have to introduce a budget? Isn't any optimization problem also a search problem in the sense that we are searching for a solution that has the property of being optimal? The catch is that the solution to a search problem should be easy to recognize, or as we put it earlier, polynomial. Given a potential solution to the TSP, it is easy to check the properties of a “is tour” that each vertex is visited exactly once and “has total length $\le b$.” But how could we check the property “optimal?”

As with SAT, there are no known polynomial-time algorithms for the TSP, despite much effort by researchers nearly every century. Of course, there is an exponential algorithm for solving it, by trying all $(n-1)!$ tours, and in Section 6.6 we saw a faster, yet still exponential, dynamic programming approach.

The minimum spanning tree (MST) problem, for which we have efficient algorithms, provides a stark contrast. To phrase it as a search problem, we are given a distance matrix and a bound $b$, and are asked to find a tree $T$ with total weight $\sum_{(i,j)}d_{ij} \le b$. The TSP can be thought of as a tough cousin of the MST problem, in which the tree is not allowed to branch and is therefore a path.$1$ This extra restriction on the structure of the tree results in a much harder problem.

## Euler and Rudrata

In the summer of 1735 Leonhard Euler (pronounced “Oiler”), the famous Swiss mathematician, was laying the bridges of the East Prussian town of Königsberg.

> Actually the TSP demands a cycle, but one can define an alternative version that seeks a path, and is not hard to see that this is as hard as the TSP itself.

# Chapter 8

## Algorithms 27

After a while, he noticed in frustration that, no matter where he started his walk, no matter how cleverly he continued, it was impossible to cross each edge once. And from this silly ambition, the field of graph theory was born.

Euler identified at once the roots of the park's deficiency. First, you turn the map of the park into a graph whose vertices are the four land masses (two islands, two banks) and whose edges are the seven bridges:

![](img/3dd1f1364df8f87b80683fc32a15b999_247_0.png)

This graph has multiple edges between two vertices—a feature we have not been allowing so far in this book, but one that is meaningful for this particular problem, since each bridge must be accounted for separately. We are looking for a path that goes through each edge exactly once (the path is allowed to repeat vertices). In other words, we are asking this question: When can a graph be drawn without lifting the pencil from the paper?

The answer discovered by Euler is simple, elegant, and intuitive: If and only if (a) the graph is connected and (b) every vertex, with the possible exception of two vertices (the start and final vertices), has even degree (Exercise 36). This is why Königs's graph was impossible: all vertices have odd degree.

To put it in terms of our concerns, let us define a search called EULER PATH: Given a graph, find a path that connects each edge exactly once. It follows from Euler's observation, and a little more thinking, that this search can be solved in polynomial time.

Almost a millennium before Euler's summer in East Prussia, a Kashmiri poet named Rudrak had such a question: Can one visit all the squares of the chessboard, without repeating any square, in one long path that ends at the starting square? This is a graph problem: the graph now has 64 vertices, and two squares are joined by an edge if a knight can go from one to the other in a single move (that is, if their coordinates differ by 2 in one dimension and by 1 in the other). See Figure 8.2 for the

# Figure 8.2 Knight's moves on a corner of a chessboard.

![](img/3dd1f1364df8f87b80683fc32a15b999_248_0.png)

corresponding to the upper left corner of the board. Can you find a knight's tour on your chessboard?

This is a different kind of search problem in graphs: we want a cycle that goes through vertices (as opposed to edges in Euler's problem), without repeating any vertex. And there is no reason to stick to chessboards; this question can be asked of any graph. Let us define the RUDRATA cycle search problem to be the following: given a graph, find a cycle that visits each vertex once—report that no such cycle exists. This problem is ominously reminiscent of the TSP, and indeed no polynomial algorithm is known for it.

There are two differences between the definitions of the Euler and Rudrata problems. The first is that Euler's problem visits edges while Rudrata's visits all vertices. But there is also the issue that one of them demands a path while the other requires a cycle. Which of these differences accounts for the huge disparity in computational complexity between the two problems? It must be the first, because we define the RUDRATA PATH problem to be just like RUDRATA CYCLE, except that the goal is to find a path that goes through each vertex. As we will soon see, there is a precise equivalence between the two versions of the Rudrata problem.

## Cuts and bisections

A cut is a set of edges whose removal leaves a graph disconnected. It is often of interest to find small cuts, and the minimum CUT problem is given, given a graph and a
