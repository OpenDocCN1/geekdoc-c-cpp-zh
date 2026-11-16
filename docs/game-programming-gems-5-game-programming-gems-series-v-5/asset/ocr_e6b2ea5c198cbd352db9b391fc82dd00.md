The algorithm performs an initial pathfinding by calling ProcessState() repeatedly. In Figure 3.8.4, the arrows show the backpointer of each node. Remember that the backpointers tell us which direction we should follow to minimize the total cost of our path.

![](bbox=[0.19, 0.22, 0.52, 0.45])

![](bbox=[0.66, 0.22, 0.93, 0.45])

In Figure 3.8.5, we show the path that is followed if we start from upper-left corner ([0] [0]) if we use a C notation and read the map as a matrix).

![](bbox=[0.42, 0.6, 0.69, 0.8])

Our agent starts following the path depicted. Suppose that when it is at location [4][1], the square at [4][2] becomes an OBSTACLE. Let's see how D* handles this. When the algorithm detects that there has been a change in the environment, it calls the function ModifyCost(x, y, value); it changes the arc cost from x to y and