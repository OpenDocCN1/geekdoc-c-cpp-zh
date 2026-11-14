![](bbox=[0.11, 0.08, 0.82, 0.3])

Figure 4.1 Schematic of one-block one-contracted Integral (1B1C) mapping. Cyan squares on left represent contracted ERIs each mapped to the labeled CUDA block of 64 threads. Orange squares show mapping of primitive ERIs to CUDA threads (green and blue boxes, colored according to CUDA warp) for two representative integrals, the first contraction over a single primitive ERI and the second involving 3^4 = 81 primitive contributions

![](bbox=[0.28, 0.41, 0.65, 0.64])

Figure 4.2 Schematic of one-thread one-contracted Integral (1T1C) mapping. Cyan squares represent contracted ERIs and CUDA threads. Thread indices are shown in parentheses. Each CUDA block (red outlines) computes 16 ERIs, with each thread accumulating the primitives of an independent contraction, in a local register