The progress of a traversal after the start vertex depends on the traversal method being used. We'll start by looking at how a depth-first search proceeds.

# Depth-First Search

After processing vertex 0, a depth-first search moves along a directed edge to one of vertex 0's neighbors. In our example, there are two possibilities: moving to vertex 1 (along the edge from 0 to 1) or moving to vertex 4 (along the edge from 0 to 4). In our example, it is not possible to move from vertex 0 to 3, or from vertex 0 to 2, because the edges go in the wrong direction. So the traversal has a choice: Move to vertex 1 or move to vertex 4. Right now we won't worry about exactly how the choice is made—let's just assume that the next vertex processed is vertex 1. After processing vertex 1, the picture looks like this:

![](bbox=[0.35, 0.365, 0.82, 0.465])

In the drawing we have highlighted the edge from vertex 0 to vertex 1 to indicate the intuitive notion of “moving from one vertex to another.” You may think of vertex 1 as being at the “leading edge” of the depth-first traversal. It is the vertex that has most recently been processed, and so we will continue pushing forward from vertex 1, moving to one of vertex 1’s unprocessed neighbors. In this example, there is only one unprocessed neighbor to consider, vertex 3. So we will move to vertex 3 and process it. At this point, we have processed three of the vertices, as shown here:

![](bbox=[0.35, 0.615, 0.82, 0.715])

to prevent going around in circles, never move forward to a marked vertex

One of vertex 3’s neighbors is vertex 0—but vertex 0 has already been marked as previously processed. So, to prevent the traversal from going around in circles, we will not move from 3 back to 0. In general, we will never move forward to a marked vertex (since it has already been processed). But we will move to vertex