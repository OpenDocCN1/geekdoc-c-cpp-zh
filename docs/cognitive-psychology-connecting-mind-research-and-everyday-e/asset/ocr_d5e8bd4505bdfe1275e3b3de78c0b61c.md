# Table 12.1: Key Terms for Newell-Simon Approach to Problem Solving

| TERM | DESCRIPTION | EXAMPLE FROM TOWER OF HANOI |
|---|---|---|
| Initial state | Conditions at the beginning of a problem. | All three discs are on the left peg. |
| Goal state | Solution to the problem. | All three discs are on the right peg. |
| Intermediate state | Conditions after each step is made toward solving a problem. | After the smallest disc is moved to the right peg, the two larger discs are on the left peg and the smallest one is on the right. |
| Operators | Actions that take the problem from one state to another. Operators are usually governed by rules. | Rule: A larger disc can't be placed on a smaller one. |
| Problem space | All possible states that could occur when solving a problem. | See *Figure 12.10*. |
| Means-end analysis | A way of solving a problem in which the goal is to reduce the difference between the initial and goal states. | Establishing subgoals, each of which moves the solution closer to the goal state. |
| Subgoals | Small goals that help create intermediate states that are closer to the goal. Occasionally, a subgoal may appear to increase the distance to the goal state but in the long run can result in the shortest path to the goal. | Subgoal 4: To free up the medium-sized disc, need to move the small disc from the middle peg back to the peg on the left. |

state, and all the possible intermediate states for a particular problem make up the **problem space**. (See Table 12.1 for a summary of the terms used by Newell and Simon.)

The problem space for the Tower of Hanoi problem is shown in *Figure 12.10*. The initial state is marked 1 and the goal state is marked 8. All of the other possible configurations of discs on pegs are intermediate states. There are a number of ways to get from the initial state to the goal state. One possibility, indicated by the red lines, involves making 14 moves. The best solution, indicated by the green lines, requires only 7 moves.

Given all of the possible ways to reach the goal, how can we decide which moves to make, especially when starting out? It is important to realize that the problem-solver does not have a picture of the problem space, like the one in *Figure 12.10*, when trying to solve the problem. According to Newell and Simon, the person has to search the problem space to find a solution, and they proposed that one way to direct the search is to use a strategy called *means-end analysis*. The primary goal of *means-end analysis* is to reduce the difference between the initial and goal states. This is achieved by creating *subgoals*—intermediate states that are closer to the goal.

Our overall goal in applying *means-end analysis* to the Tower of Hanoi problem is to reduce the size of the difference between initial and goal states. An initial goal would be to move the large disc that is on the left over to the peg on the right. However, if we are to obey the rules, we can’t accomplish this in just one step, because we can move only one disc at a