Figure 7. A neighborhood of hexagonally sampled pixels.

It seems we have to give up on 4-connectedness, since it leads to a paradox. Let’s go to 8-connected. Now, the foreground is closed, right? But now, the inside and outside are also connected! How can that be? If the region is closed, the inside and outside must (logically) be separate. Therefore, 8-connectedness does not work either.

For this particular paradox, there is a fix, at least sort of a fix, which is to use one definition (8- or 4-connected) for the foreground and the other for the background. This fix works for binary images, but when we get to images with more than two levels of brightness, these discretization problems occur again. This example is presented to illustrate that in digital images, intuition is not always correct. There are lots of other examples of similar problems involving, for example, the measure of the perimeter of regions. Just be aware that, as in life, weird things happen and intuition does not always hold.

# A Variation on Sampling: Hexagonal Pixels

Traditionally, electronic imaging sensors have been arranged in rectangular arrays mainly because an electron beam needed to be swept in a raster-scan way, and more recently because it is slightly more convenient to arrange semiconductor devices in a rectangular organization. However, as we saw above, rectangular arrays introduce an ambiguity in attempts to define neighborhoods. On the other hand, hexagonal pixels provide an ideal solution to the ambiguity problem.

We could easily imagine imaging sensors that use hexagonally organized pixel arrays. Hexagons are the minimum-energy solution when a collection of tangent circles with flexible boundaries are subject to pressure. The beehive is the best-known such naturally occurring organization, but many others occur too, including the organization of cones in the human retina. We see in Figure 4.7 that there are no connectivity paradoxes in hexagonal connectivity analysis: every pixel has exactly six neighbors, and the distance between each pixel and its immediate neighbors is the same along any of the six main directions of the hexagonal tessellation.

# 4.3 The Image as a Surface

In this section, we consider the problem of interpreting the image as a surface in a 3D space. Thinking of an image in this way will allow us to conceive of image properties as heights.