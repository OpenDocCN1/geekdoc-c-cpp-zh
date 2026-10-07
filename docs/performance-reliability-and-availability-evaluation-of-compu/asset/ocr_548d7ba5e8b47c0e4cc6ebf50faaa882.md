# 462 Performance, Reliability, and Availability Evaluation of Computational Systems

The confidence interval, the mean execution time (met), and the average MFLOPS (amflops) with 95% of confidence were calculated using the nonparametric bootstrap-strap. These confidence intervals are depicted below:

$met \in (1.0166s, 1.0430s)$

and

$amflops \in (768.9516MFLOPS, 787.2465MFLOPS)$,

Similar exercise can be performed for the open-source benchmarks as some of the following.

# Livermore Loops

The Livermore Loops is a benchmark, originally written in Fortran, composed of twenty-four kernels. McMahon implemented the Livermore loops at Livermore National Laboratories [268]. This benchmark executes the 24 kernels three times at different loops to produce short, medium, and long vector measurements. Beside, each loop implements a specific type of scientific programming constructs applied at the laboratory. The performance measurements are depicted in MFLOPS (or multiples of), and statistics such as are reported for minimum, maximum, and three means: arithmetic, geometric, and harmonic are provided. Since the original implementation, the Livermore Kernels were also implemented in many other languages such as C, C++, and CUDA.

We implemented a C program (livermore.c) that sequentially executed twenty-three out of twenty-four kernels of the Livermore loops available at [242]. Kernel 13 was not considered. The time to execute the program was measured by adopting the same function and structure when evaluating Whetstone and Linpack. The C program was executed one hundred times, and each execution time (seconds) was stored in a livermore.txt file (See Appendix D). For performing the measurement, we adopted the script (scriptlivermore) below.

scriptlivermore

```
printf "Livermore Results \n" >> livermore_result.txt;
for i in {1..100}
do
livermore >> livermore_result.txt;
done
```

The execution times of the sample are shown in Table 24.7. In addition, Table 24.8 shows the statistical summary for the execution times measured.