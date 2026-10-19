# 21

# Wave Equations I: Strings and Membranes

In this chapter and in the next, we explore the numerical solution of several PDEs that yield waves as solutions. If you have skipped the discussion of the heat equation in Chapter 20, then this chapter will be the first example of how initial conditions are propagated forward in time with a time-stepping or leapfrog algorithm. An important aspect of this chapter is its demonstration that once you have a working algorithm for solving a wave equation, you can include considerably more physics than is possible with analytic treatments. First, we deal with a number of aspects of 1D waves on a string, and then with 2D waves on a membrane. In the next chapter, we look at quantum wave packets and E&M waves. In Chapter 24, we look at shock and solitary waves.

# 21.1

# A Vibrating String

Problem Recall the demonstration from elementary physics in which a string tied down at both ends is plucked “gently” at one location and a pulse is observed to travel along the string. Likewise, if the string has one end free and you shake it just right, a standing-wave pattern is set up in which the nodes remain in place and the antinodes move just up and down. Your problem is to develop an accurate model for wave propagation on a string, and to see if you can set up traveling- and standing-wave patterns.

# 21.2

# The Hyperbolic Wave Equation (Theory)

Consider a string of length L tied down at both ends (Figure 21.1a). The string has a constant density ρ per unit length, a constant tension T, no frictional forces acting on it, and a tension that is so high that we may ignore sagging as a result of

1) Some similar but independent studies can also be found in Rawitscher et al. (1996).