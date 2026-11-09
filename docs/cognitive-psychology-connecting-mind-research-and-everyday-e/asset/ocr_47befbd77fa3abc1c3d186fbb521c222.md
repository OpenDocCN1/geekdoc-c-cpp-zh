![](bbox=[0.145, 0.045, 0.88, 0.405])

**Figure 12.10** Problem space for the Tower of Hanoi problem. The green lines indicate the shortest path between the initial state (1) and the goal state (8). The red lines indicate a longer path. (*Source: Based on K. Dunbar, Problem solving, in W. Bechtel & G. Graham, Eds., A companion to cognitive science, pp. 289–298, London: Blackwell, 1998.*)

time and can't move a disc if another disc is on top of it. To solve the problem we therefore set a series of subgoals, some of which may involve a few moves:

+   - *Subgoal 1:* Free up the large disc so we can move it onto peg 3. Do this by (a) removing the small disc and placing it on the third peg (Figure 12.11a; this is state 2 in the problem space in Figure 12.10), (b) Remove the medium disc and place it on the second peg (Figure 12.11b; state 3 in the problem space). This completes the subgoal of freeing up the large disc.
+   - *Subgoal 2:* Free up the third peg so we can move the large disc onto it. Do this by moving the small disc onto the medium one (Figure 12.11c; state 4 in the problem space).
+   - *Subgoal 3:* Move the large disc onto peg 3 (Figure 12.11d; state 5 in the problem space).
+   - *Subgoal 4:* Free up the medium disc.

Now that we have reached state 5 in the problem space, let's stop and decide how to achieve subgoal 4, freeing up the medium disc. We can move the small disc either onto peg 3 or onto peg 1. These two possible choices illustrate that to find the shortest path to the goal, we need to look slightly ahead. When we do this, we can see that we should not move the small disc to peg 3, even though it appears to reduce the difference between the initial and goal states. Moving to peg 3 is the wrong move, because that would block moving the medium disc there, which would be our next subgoal. Thus, we move the disc back to peg 1 (state 6), which makes it possible to move the medium disc to peg 3 (state 7), and we have almost solved the problem! This procedure of setting subgoals and looking slightly ahead often results in an efficient solution to a problem.

Why is the Tower of Hanoi problem important? One reason is that it illustrates means–end analysis, with its setting of subgoals, and this approach can be applied to real-life situations. For example, I recently had to plan a trip from Pittsburgh to Copenhagen. Remember