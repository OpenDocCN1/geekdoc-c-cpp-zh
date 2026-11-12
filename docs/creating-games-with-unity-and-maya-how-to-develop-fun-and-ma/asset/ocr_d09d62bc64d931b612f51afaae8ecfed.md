![](bbox=[0.08, 0.08, 0.92, 0.3])

**FIGURE 8.54** Continued extrusions to the belt.

# ### Arms

In the previous steps we carefully created a hole from which to extrude the arms. It is important that this ring is carefully constructed since it will define how many polys will be used to describe the roundness of the arm. Remember these polygons will be the basis of not only the arm, but the hand as well. In this kind of modeling, you are looking to find the balance of having just the right amount of polygons to describe the surface, without having too many or too few; it is a skill that simply takes time to develop.

The important thing to note is that there are 10 edges. This will allow for four fingers later. If you have more or less than this, now is a good time to adjust. Adjusting can include adding new vertices by using the Split Polygon tool or Insert Edge Loop tool if you need additional edges, or selecting and deleting edges if you need fewer. It's also worth noting that the spacing of these 10 edges should be fairly even. Adjust the spacing now if you have undesired clusters because well-spaced edges will save you loads of time as you work down the arm.

**Step 75:** Select the ring of edges that is around the arm hole, and begin extruding out to create the form that is the arm. Figure 8.55 shows two extrusions. Note that the second extrusion is a really long one that anticipates us going back to add needed detail.

**Step 76:** Using the Insert Edge Loop tool, add a subdivision around the middle forearm, and then three around the elbow area (Figure 8.56).

# ### Why?

At first glance, it seems rather silly to be dropping so much of the polygon budget on the elbow; I mean, surely there isn't that much visually happening there, right? Well, visually this is true, but remember that these meshes are going to be deformed by joints. Consider the following simplified illustration.

Figure 8.57 shows a simple joint chain and the real-world equivalency. Figure 8.58 shows how an elbow would deform if there was a single subdivision at the elbow. See the compression that occurs there? Figure 8.59 shows the