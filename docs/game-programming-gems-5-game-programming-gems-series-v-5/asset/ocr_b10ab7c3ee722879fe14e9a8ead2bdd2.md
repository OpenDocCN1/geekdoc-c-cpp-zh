To determine the flag for each link in a preprocessing step, we perform ray casts along each side of the link at the appropriate heights (Figure 3.1.1). Once we’ve determined the applicable cover or lack thereof for each edge, we can store that information in less than one byte per triangle (since there are only two bits of information per edge).

![](bbox=[0.3, 0.19, 0.75, 0.41])

These two simple cover distinctions (standing and crouching) assume human-sized opponents. To accommodate a wider variety of heights in the NPCs searching for cover, simply increase the number of cover ranges above two (a flag for each meter of cover, for instance) or store the height of the link in the navigation graph (which has other potential applications, like determining if an NPC can climb or jump to the linked triangle).

# Testing a Triangle for Cover

To determine if a given triangle is acceptable as a cover position, we have to do two things:

+   1. Test for a straight line path from the center of a given triangle to the target point (that we wish to be in cover from). This can use simplified two dimensional line segment intersections tests, as in Snook’s article [Snook02].
+   2. If the triangle does not have a straight path to the target point, find the edge that is between the center of this triangle and the target; if that link was flagged in our preprocessing step as crouching or standing cover, this triangle can be considered to be in cover from the target.

# Limitations

With this type of graph and cover test, we do face a couple of limitations. To start, because the navigation is preprocessed, our algorithm can only find static cover (the list of large enough dynamic objects can then be iterated through quickly for additional cover points).

In addition, the two-dimensional math for fast line-of-sight operations limits us to wall-based cover. The ground itself will never be used as cover, as in the case of a hill that lies between an NPC and its target. For many environments, such as urban settings or interiors, this is not much of a concern.