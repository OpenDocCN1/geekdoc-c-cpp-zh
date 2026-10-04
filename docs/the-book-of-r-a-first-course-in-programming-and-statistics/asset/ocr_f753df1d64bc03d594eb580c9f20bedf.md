+   b. Using the model from (a), construct a z-matrix of predicted mean daily temperature based on a 50 × 50 evaluation grid in both wind speed and ozone.
c. Create a pixel image of the response surface, superimposing the raw observations as per the following:
- A graphics device should be initialized based on bottom, left, top, and right margins of 5, 4, 4, and 6, respectively.
- 20 colors from the built-in topo.colors palette should be used to produce the image; include tidy axes titles.
- Revisit the normalize function defined in Section 25,1.4 and use the built-in gray function to generate a vector of gray (refer to Section 25,1.2) based on the normalized raw temperature observations. Superimpose the raw observations based on wind speed and ozone onto the pixel image, using the gray color vector to indicate the corresponding observations.
- Two separate calls should then be made to colorleg of the shape package. The first should appear in the space on the right margin, referencing the surface itself. The second should use the built-in gray.colors function, setting the optional arguments start=0 and end=1, to generate 10 shades of gray for use in the legend that references the raw temperature observations of the superposed points. This legend should reside on top of the pixel image, in the upper-right quadrant where there are no raw observations. Both legends should have appropriate titles, and you may need to experiment a little with the posx and posy arguments to find satisfactory placement.

My result of this plotting exercise appears here.

![](bbox=[0.388, 0.646, 0.858, 0.876])

Defining Colors and Plotting in Higher Dimensions 677