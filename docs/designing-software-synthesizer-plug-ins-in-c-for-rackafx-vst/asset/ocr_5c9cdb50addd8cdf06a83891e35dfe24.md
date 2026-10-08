the center position, there is an equal vector mix of the sources.

![](bbox=[0.187, 0.068, 0.812, 0.189])

Figure 11.4: The vector mix moves exponentially as the joystick moves linearly.

![](bbox=[0.187, 0.243, 0.812, 0.347])

Figure 11.5: The 50/50 mix ratios between adjacent vertices is found midway between the outer diamond edge.

![](bbox=[0.19, 0.417, 0.809, 0.659])

Figure 11.6: A few more sample joystick-position-to-mix ratios show the exponential mapping.

Figure 11.6 shows a few more positions of the joystick and the non-linear mapping from the (x,y) joystick coordinates to the mixing variables.

# Vector Mix Calculation

Kordi provides the vector mix calculation for software developers. It is available at Dan Phillips' website, which is also full of Wavastream resources. See the Bibliography for the link. The user does not see the coordinates, only the mix ratios. If we use the literal joystick coordinate system, where the coordinates of the A vertex are (-1,0), the B vertex coordinates are (0, 1), and so on, the calculation first involves rotating the diamond shape by -45 degrees (i.e. clockwise) to produce a proper square shape. Figure 11.7 shows how this re-maps the literal vector joystick coordinates.