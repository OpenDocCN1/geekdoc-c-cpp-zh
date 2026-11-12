# **PROJECT**

# ## Chromatic Polynomials

# ### Purpose

In previous courses, you may have learned about how coloring vertex-edge graphs can help you solve problems. You probably found that you and your classmates often colored the same graph differently. In this project, you will investigate the number of ways a graph can be colored using *k* colors.

# ### Directions

A *k*-coloring of a network or vertex-edge graph is an assignment of *k* colors to the vertices so that no two vertices connected by an edge have the same color. In the past, you have explored the existence of a coloring using a minimum number of colors. (See Course 1, Unit 4, Lesson 2.) Shown at the right are two different colorings of a graph on 4 vertices using 3 colors. Two colorings are different if at least one vertex has a different color.

![](bbox=[0.706, 0.366, 0.812, 0.58])

+   1. How many different 3-colorings are there of the graph shown below? Explain your reasoning.

![](bbox=[0.348, 0.536, 0.389, 0.572])

+   2. The function that gives the number of *k*-colorings for a graph *G* is called the chromatic polynomial and is denoted by $C_G(k)$. Think about the chromatic polynomials for the following two graphs.

![](bbox=[0.241, 0.658, 0.331, 0.724])

Graph on 4 vertices with no edges

![](bbox=[0.579, 0.659, 0.66, 0.724])

Complete graph on 4 vertices (every edge)

+   **a.** Let *G* be a graph of 4 vertices with no edges. Explain why the chromatic polynomial for a graph *G* of 4 vertices with no edges is $C_G(k)=k^4$.

+   **b.** Explain why the chromatic polynomial for a complete graph *G* on 4 vertices is $C_G(k)=k(k-1)(k-2)(k-3)$. What are the zeros for this polynomial? Explain why the chromatic polynomial must be zero for these values of *k*.

+   **c.** What is the chromatic polynomial for a graph *G* on *p* vertices with no edges? What is the chromatic polynomial for a complete graph *G* on *p* vertices?