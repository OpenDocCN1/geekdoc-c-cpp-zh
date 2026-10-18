# FIGURE 23.21

Memory Access Pattern source view.

Looking at the patterns report in bottom of Figures 23.20 and 23.21 you can see that bad memory access comes from:

+   - Problems P1, P2, & P3 (colored yellow). Three simultaneous packed loads of three mutually related references at 3*m, 3*m+1, 3*m+2 positions—with additional shift of 3 every next scalar iteration (that’s why it’s classified as stride-3).
+   - Problem P12 has an “unpredictable” or random stride access coming from the swapping routine. It’s not surprising to find random access here, as the address to be swapped is defined by the value in ilnext (being a complex function of lbv array values and m)—leading to a pure form of indirect referencing.

With such a terrible dynamic memory access pattern, at runtime we don’t achieve the static estimated gain of 1.22; in fact, we don’t experience any performance boost at all.

# A final MAP analysis

Let’s try to investigate vectorization for the “outer loop” now—hoping it proves to be better from memory usage perspective. First, we rerun MAP analysis for the outer loop (1-loop). Surprisingly MAP results are much more promising (see Figure 23.22); the random indirect referencing seems to have

![](bbox=[0.115, 0.48, 0.85, 0.71])

# FIGURE 23.22

Memory Access Patterns Analysis for the outer loop in fPropagationSwap.