tic fractals. Modeling such distributions have subtle issues that are somewhat unusual in the context of common data analysis.

![](bbox=[0.101, 0.152, 0.93, 0.632])

**FIGURE 2.5:** Comparing the Tanimoto (above) and Baroni-Urbani/Buser (below) coefficient distributions, given all binary strings of length 5. The right hand of the distribution of the Baroni is slightly larger and nearer 1, but it still very discrete and has fewer possible values (9 to the Tanimoto's 10).

With careful programming the Baroni-Urbani/Buser measure is roughly 40 to 50% slower than a fast implementation of the Tanimoto measure. This makes it competitive with the Tanimoto for large scale compound selection and related similarity searching and clustering applications, and hence its more recent widespread use, as it has slightly better distributional properties than the Tanimoto.

# 2.6.1.3 The Simple Matching Coefficient

The simple matching coefficient is just that: just count the bits turned on in common between A and B (namely c as defined for the Tanimoto measure),