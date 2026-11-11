the real world, accepting limitations to achieve computational efficiency. The hardest problems in animation involve artificial intelligence for planning realistic character motion, which is beyond the scope of this chapter.

+   - 35.1 Introduction ... 963
+   - 35.2 Motivating Examples ... 966
+     - 35.2.1 A Walking Character (Key Poses) ... 966
+     - 35.2.2 Firing a Cannon (Simulation) ... 969
+     - 35.2.3 Navigating Corridors (Motion Planning) ... 972
+     - 35.2.4 Notation ... 973
+   - 35.3 Considerations for Rendering ... 975
+     - 35.3.1 Double Buffering ... 975
+     - 35.3.2 Motion Perception ... 976
+     - 35.3.3 Interlacing ... 978
+     - 35.3.4 Temporal Aliasing and Motion Blur ... 980
+     - 35.3.5 Exploiting Temporal Coherence ... 983
+     - 35.3.6 The Problem of the First Frame ... 984
+     - 35.3.7 The Burden of Temporal Coherence ... 985
+   - 35.4 Representations ... 987
+     - 35.4.1 Objects ... 987
+     - 35.4.2 Limiting Degrees of Freedom ... 988
+     - 35.4.3 Key Poses ... 989
+     - 35.4.4 Dynamics ... 989
+     - 35.4.5 Procedural Animation ... 990
+     - 35.4.6 Hybrid Control Schemes ... 990
+   - 35.5 Pose Interpolation ... 992
+     - 35.5.1 Vertex Animation ... 992
+     - 35.5.2 Root Frame Motion ... 993
+     - 35.5.3 Articulated Body ... 994
+     - 35.5.4 Skeletal Animation ... 995
+   - 35.6 Dynamics ... 996
+     - 35.6.1 Particle ... 996
+     - 35.6.2 Differential Equation Formulation ... 997
+     - 35.6.3 Piecewise-Constant Approximation ... 999
+     - 35.6.4 Models of Common Forces ... 1000
+     - 35.6.5 Particle Collisions ... 1008
+     - 35.6.6 Dynamics as a Differential Equation ... 1012
+     - 35.6.7 Numerical Methods for ODEs ... 1017
+   - 35.7 Remarks on Stability in Dynamics ... 1020
+   - 35.8 Discussion ... 1022
+   - 36 Visibility Determination ... 1023

Efficient determination of the subset of a scene that affects the final image is critical to the performance of a renderer. The first approximation of this process is conservative determination of surfaces visible to the eye. This problem has been addressed by algorithms with radically different space, quality, and time bounds. The preferred algorithms vary over time with the cost and performance of hardware architectures. Because analogous problems arise in collision detection, selection,