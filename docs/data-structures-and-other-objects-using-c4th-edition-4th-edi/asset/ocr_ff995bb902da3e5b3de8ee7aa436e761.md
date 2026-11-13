![](bbox=[0.356, 0.163, 0.735, 0.269])

The shaded vertices have already been processed.

Does $v_3$ have any more unmarked neighbors?

Vertex 3 has no more unmarked neighbors (thank goodness!). So back we go to the previous vertex—vertex 1—to check whether it has any unmarked neighbors:

![](bbox=[0.356, 0.363, 0.735, 0.469])

The shaded vertices have already been processed.

Does $v_1$ have any more unmarked neighbors?

You can see that the leading edge of the search is now at $v_1$, and that $v_1$ has no more unmarked neighbors, so back we go to vertex 0, to see if it has any unfinished business. This situation is drawn here:

![](bbox=[0.356, 0.563, 0.735, 0.669])

The shaded vertices have already been processed.

Does $v_0$ have any more unmarked neighbors?

From vertex 0 we can still travel to the unmarked vertex 4 and process it, as shown here:

![](bbox=[0.356, 0.743, 0.735, 0.849])

The shaded vertices have already been processed.