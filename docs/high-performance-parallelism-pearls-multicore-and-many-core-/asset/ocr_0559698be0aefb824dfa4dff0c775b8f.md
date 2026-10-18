# CHAPTER 9 Wilson Dslash Kernel from Lattice QCD Optimization ............... 139

+   Transcendental functions........................................................... 119
+   Reuse as much as possible and reinvent as little as possible....................... 119
+   Subexpression evaluation ........................................................... 120
+   SIMD parallelism—Vectorization ..................................................... 122
+   Define and use vector data........................................................... 122
+   Vector arithmetic operations....................................................... 123
+   Vector function call............................................................... 124
+   Branch statements............................................................... 124
+   Calling the vector version and the scalar version of the program ............... 126
+   Vectorization by annotating the source code: #pragma SIMD ..................... 129
+   C/C++ vector extension versus #pragma SIMD....................................... 129
+   Thread parallelization........................................................... 130
+   Memory allocation in NUMA system.................................................. 132
+   Thread binding and affinity interface ............................................ 133
+   Scale from multicore to many-core ............................................... 133
+   Summary......................................................................... 136
+   For more information ............................................................. 136

+   The Wilson-Dslash kernel........................................................... 140
+   Performance expectations........................................................... 143
+   Refinements to the model........................................................... 144
+   First implementation and performance ............................................. 146
+   Running the naive code on Intel Xeon Phi coprocessor ............................ 149
+   Evaluation of the naive code....................................................... 150
+   Optimized code: QPhiX and QphiX-Codegen.......................................... 151
+   Data layout for vectorization..................................................... 151
+   3.5D blocking ................................................................... 153
+   Load balancing ................................................................ 154
+   SMT threading................................................................... 155
+   Lattice traversal ............................................................... 156
+   Code generation with QphiX-Codegen............................................... 157
+   QphiX-codegen code structure...................................................... 159
+   Implementing the instructions..................................................... 159
+   Generating Dslash............................................................... 160
+   Prefetching..................................................................... 162
+   Generating the code.............................................................. 163
+   Performance results for QPhiX.................................................... 164
+   Other benefits ................................................................ 166
+   The end of the road?.............................................................. 168
+   For more information ............................................................. 169