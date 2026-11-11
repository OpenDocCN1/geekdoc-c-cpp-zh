+   - 29.5 Scattering, Revisited ...... 792
+   - 29.6 A Worked Example ...... 793
+   - 29.7 Solving the Rendering Equation ...... 796
+   - 29.8 The Classification of Light-Transport Paths ...... 796
+     - 29.8.1 Perceptually Significant Phenomena and Light Transport ...... 797
+   - 29.9 Discussion ...... 799
+   - 29.10 Exercise ...... 799

# ## 30 Probability and Monte Carlo Integration ...... 801

Probabilistic methods are at the heart of modern rendering techniques, especially methods for estimating integrals, because solving the rendering equation involves computing an integral that's impossible to evaluate exactly in any but the simplest scenes. We review basic discrete probability, generalize to continuum probability, and use this to derive the single-sample estimate for an integral and the importance-weighted single-sample estimate, which we'll use in the next two chapters.

+   - 30.1 Introduction ...... 801
+   - 30.2 Numerical Integration ...... 801
+   - 30.3 Random Variables and Randomized Algorithms ...... 802
+     - 30.3.1 Discrete Probability and Its Relationship to Programs ...... 803
+     - 30.3.2 Expected Value ...... 804
+     - 30.3.3 Properties of Expected Value, and Related Terms ...... 806
+     - 30.3.4 Continuum Probability ...... 808
+     - 30.3.5 Probability Density Functions ...... 810
+     - 30.3.6 Application to the Sphere ...... 813
+     - 30.3.7 A Simple Example ...... 813
+     - 30.3.8 Application to Scattering ...... 814
+   - 30.4 Continuum Probability, Continued ...... 815
+   - 30.5 Importance Sampling and Integration ...... 818
+   - 30.6 Mixed Probabilities ...... 820
+   - 30.7 Discussion and Further Reading ...... 821
+   - 30.8 Exercises ...... 821

# ## 31 Computing Solutions to the Rendering Equation: Theoretical Approaches ...... 825

The rendering equation can be approximately solved by many methods, including ray tracing (an approximation to the series solution), radiosity (an approximation arising from a finite-element approach), Metropolis light transport, and photon mapping, not to mention basic polygonal renderers using direct-lighting-plus-ambient approximations. Each method has strengths and weaknesses that can be analyzed by considering the nature of the materials in the scene, by examining different classes of light paths from luminaries to detectors, and by uncovering various kinds of approximation errors implicit in the methods.

+   - 31.1 Introduction ...... 825
+   - 31.2 Approximate Solutions of Equations ...... 825
+   - 31.3 Method 1: Approximating the Equation ...... 826
+   - 31.4 Method 2: Restricting the Domain ...... 827
+   - 31.5 Method 3: Using Statistical Estimators ...... 827
+     - 31.5.1 Summing a Series by Sampling and Estimation ...... 828