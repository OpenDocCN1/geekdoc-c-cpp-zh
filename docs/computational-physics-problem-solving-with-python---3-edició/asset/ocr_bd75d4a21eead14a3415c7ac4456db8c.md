We see that the extra white space in Figure 16.1b leads to a density that is 3/4 that of the previous stage. For the structure in Figure 16.1c, we obtain

ρ(L = 4r) ∝ (M = 9m)/(4r)² = 9/16 m/r² = (3/4)² ρ₀  (Figure 16.1b-C).  (16.7)

We see that as we continue the construction process, the density of each new structure is 3/4 that of the previous one. Interesting. Yet in (16.2) we derived that

ρ ∝ C L^{d_f - 2}.  (16.8)

Equation 16.8 implies that a plot of the logarithm of the density ρ vs. the logarithm of the length L for successive structures yields a straight line of slope

d_f - 2 = Δ log ρ / Δ log L.  (16.9)

As applied to our problem,

d_f = 2 + Δ log ρ(L) / Δ log L = 2 + [log 1 - log 3/4] / [log 1 - log 2] ≈ 1.58496.  (16.10)

As is evident in Figure 16.1, as the gasket grows larger (and consequently more massive), it contains more open space. So despite the fact that its mass approaches infinity as L → ∞, its density approaches zero! And because a 2D figure like a solid triangle has a constant density as its length increases, a 2D figure has a slope equal to 0. Because the Sierpiński gasket has a slope d_f - 2 ≈ -0.41504, it fills space to a lesser extent than a 2D object but more so than a 1D object; it is a fractal with dimension 1.6.

# 16.3
Growing Plants (Problem 2)

It seems paradoxical that natural processes subject to chance can produce objects of high regularity and symmetry. For example, it is hard to believe that something as beautiful and graceful as a fern (Figure 16.2a) has random elements in it. Nonetheless, there is a clue here in that much of the fern’s beauty arises from the similarity of each part to the whole (self-similarity), with different ferns similar but not identical to each other. These are characteristics of fractals. Your problem is to discover if a simple algorithm including some randomness can draw regular ferns. If the algorithm produces objects that resemble ferns, then presumably you have uncovered mathematics similar to that responsible for the shapes of ferns.

# 16.3.1
Self-Affine Connection (Theory)

In (16.4), which defines mathematically how a Sierpiński gasket is constructed, a scaling factor of 1/2 is part of the relation of one point to the next. A more general