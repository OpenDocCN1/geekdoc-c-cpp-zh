The actual traverse_maze function is given in Figure 9.8 on page 457. It follows our pseudocode quite closely. You might enjoy knowing that the magic tapestry really does exist in a book called Castle Roogna (Ballantine Books) by Piers Anthony. The hero of the book actually becomes part of the tapestry, whereupon his quest leads him to a smaller version of the same tapestry.

# The Recursive Pattern of Exhaustive Search with Backtracking

The traverse_maze function of Figure 9.8 follows a recursive pattern that you may find useful elsewhere. The pattern is useful when a program is searching for a goal within a space of individual points that have connections between them. In the maze problem, the “points” are the individual squares of the maze, and the “connections” are the possible steps that the explorer can take in the four compass directions. Later you’ll run into many data structures that have the form of “points and connections.”

The task of searching such a structure can often follow this pattern:

+   - Start by marking the current point in some way. In the maze, the mark was obtained by asking the explorer to write her name on the ground. The purpose of the mark is to ensure that we don’t mistakenly return to this point and end up going around in circles, continually returning to this same spot. This marking step is but always necessary; sometimes there are other mechanisms to prevent unbounded repetitions of searching the same direction.

+   - Check whether the current point satisfies the goal. If so, return some value that indicates the success of the search.

+   - On the other hand, if the current point does not satisfy the goal, then one by one examine the other points that are connected to the current point. For each such point, check to see whether the point is marked; if so, we can ignore the point because we have already been there. On the other hand, if a connected point is not marked, then make a recursive call to continue the search from the connected point onward. If the recursive call finds the goal, then we won’t bother checking any other points, but if the recursive call fails, then we will check each of the other unmarked connected points by further recursive calls.

This pattern is called exhaustive search with backtracking. The term exhaustive search means that all possibilities are tried. Backtracking is the process of a recursive call returning without finding the goal. When such a recursive call returns, we are back where we started, and we can explore other directions with further recursive calls.

Exhaustive search with backtracking is most useful when the known search space doesn’t get too large. But even with huge search spaces, programmers