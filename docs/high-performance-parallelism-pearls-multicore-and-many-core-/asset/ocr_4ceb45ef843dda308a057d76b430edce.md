# ANALYZING THE LATTICE BOLTZMANN CODE

Figure 23.4 shows the initial analysis of the DL_MESO code using the vectorization advisor survey feature of Intel Advisor XE. Depending on the input data set characteristics, such as the number of fluids or collision scheme type, the hotspots’ distribution varies significantly.

The hotspots distribution has a “flat profile” pattern, which is fairly common for physics simulation codes, and contains a large number of hotspots, each taking only 3-5% of the time. Optimizing programs with this kind of “flat profile” can be time consuming, as you have to individually profile and develop each of the many hotspots.

Normally, when you start any optimization work, you should work on parts of the code that contribute most to the runtime. That is the biggest hotspot, but in our case, we chose to go in the reverse order, because we incrementally want to introduce different features of the Vectorization Advisor in the chapter. In fact, we even skip the third hotspot in fGetSpeedSite, because the fourth hotspot will serve our purposes better.

In this chapter, we look at three of the four hottest loops:

+   - lbpSUB:744 in fGetEquilibriumF calculates the equilibrium for compressible fluids
+   - lbpGET:42 in fGetOneMassSite calculates mass density
+   - lbpSUB:1247 in fPropogationSwap moves particles to neighboring grid points

# OPTIMIZING THE COMPUTE EQUILIBRIUM LOOP (lbpSUB:744)

In this section, we use the Advisor Survey Analysis to look at the constituent parts of the loop in fGetEquilibriumF, and then fix vectorization inefficiency by padding some of the data structures.

![](bbox=[0.115, 0.56, 0.86, 0.815])

FIGURE 23.4

The results of an initial analysis.