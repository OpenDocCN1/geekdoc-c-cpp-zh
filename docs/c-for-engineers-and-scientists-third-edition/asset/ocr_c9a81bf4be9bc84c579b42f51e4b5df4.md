begins the process of defining a more complicated problem as a set of smaller, more manageable tasks. Each of these tasks can be further subdivided or refined into even smaller tasks, if required. After the tasks are well defined, the actual work of coding can begin, starting with a task, in any order. If there are more tasks than one programmer can handle, they can be distributed among many programmers as necessary. This workload distribution is equivalent to having many people work on a large research project, with each person responsible for a specific or project component. A general outline applicable to many engineering and scientific tasks is the following algorithm:

# Get the inputs to the problem
Calculate the desired result
Report the results of the calculation

These three tasks are the primary responsibilities of every program, and this algorithm is referred to as the problem-solver algorithm. Figure 6.10 shows a first-level structure diagram of this algorithm.

![](bbox=[0.331, 0.38, 0.668, 0.513])

**Figure 6.10** The problem-solver algorithm

Each task in the problem-solver algorithm can be worked on independently as a function—sort of “mini” C++ program that is easier to complete than a whole program. Each function can be refined and coded in any order, although completing the input section first makes testing and development easier. Next, you apply this development procedure to the programming problem of converting rectangular coordinates to their polar equivalents.

# **Step 1** Problem Definition

A program is to be written to convert a point's rectangular (x,y) coordinates into polar form. That is, given an x and y position on a Cartesian coordinate system, shown in Figure 6.11, you must calculate the distance from the origin, $r$, and the angle from the x-axis, $	heta$, specified by the point. The values of $r$ and $	heta$ are referred to as the point's polar coordinates.

When the x and y coordinates of a point are known, the equivalent $r$ and $	heta$ coordinates can be calculated using these formulas:

```
$r = \sqrt{x^2 + y^2}$
$\theta = \tan^{-1}(y/x) \quad x \neq 0$
```

You begin developing your program with an outline of what the program is to accomplish. You can construct an initial pseudocode description by applying the problem-solver algorithm