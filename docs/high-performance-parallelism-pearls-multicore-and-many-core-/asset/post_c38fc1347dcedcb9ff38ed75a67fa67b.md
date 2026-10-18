
One technique we can apply to this code is to increase the loop iterations count to become a multiple of VL, i.e., 20 in our case—see Figure 23.7. This technique is called “data padding” and this is exactly what Advisor explicitly suggests in the “Recommendations” window for this loop (as seen in Figure 23.9). In order to “pad” the data we need to increase the size of the arrays `feq[]`, `lbv[]` and `lbw[]` so that accessing the (unused) 20th location will not cause a segmentation violation or similar problem.

Figure 23.8 gives an example of the change that is needed. The value `nq_full_width` hard codes the padding value to be `lbsy.nq + 1`, but a more elegant and portable way could be to replace 1 with VL - (`lbsy.nq` mod VL).

You will also see that we have added the `#pragma loop count (20)` directive. By telling the compiler what the loop count will be, the compiler sees that the count is a multiple of the vector length and optimizes code generation for particular trip count value so that scalar remainder invocation code is omitted in runtime.

In the DL_MESO code, there are a number of similar equilibrium distribution code constructs that can be modified in the same way. In our example, we modified three other loops in the same source file and achieved a speedup of 15% on each loop.

```cpp
int nq_full_width = lbsy.nq;
    if(lbsy.nq != 0)
        nq_full_width = lbsy.nq + 1;

    if(lbsy.nq != 0) {
        lbw = new double[nq_full_width];  // was [lbsy.nq]
    }
```

**FIGURE 23.7** Code listing—example of code changes to memory allocation, with modifications shown in bold.

```cpp
#pragma loop count (20)
for(int i=0; i<lbsy.nq + 1; i++)
{
    uv = lbv[i*3] * v[0]
        + lbv[i*3+1] * v[1]
        + lbv[i*3+2] * v[2];

    feq[i] = rho * lbw[i]
        * (1 + 3.0 * uv + 4.5 * uv * uv - 1.5 * modv);
}
```

**FIGURE 23.8** Code listing—the optimized loop, with modifications shown in bold.

![](img/16cb41208935c5f22dd1044f03f2e31b_500_0.png)

**FIGURE 23.9** The Vectorization Advisor Recommendations for padding the data.

## ANALYSIS OF THE CALCULATE MASS DENSITY LOOP (lbgPET.cpp:42)

In this section, we use Advisor to help spot an alignment issue of the loop in `fGetOneMassSite`, and then fix the problem by adding pragmas to the source code.

### The fGetOneMassSite function

Figure 23.10 shows the code for the mass density calculations. The starting position in the grid is passed into the function `fGetOneMassSite` via the parameter `startpos`. The calculated mass is returned to the calling function.

```cpp
double fGetOneMassSite(double* startpos)
{
    double mass=0.0;
    double *pt1;
    pt1= startpos;
    for(int i=0; i<lbsy.nq; i++) {
        mass += *pt1;
        pt1 ++;
    }
    pt1 = NULL;
    return mass;
}
```

**FIGURE 23.10** Code listing—calculating the mass density.

### Advisor survey

Despite the simplicity of the code, in our tests this function was the number two hotspot, and even in other test cases it often fell within the top five hotspots of the Survey Analysis—as in Figure 23.11. In the Analysis results you can see that there are four instances of the loop, those four versions being created by code in-lining that the compiler has carried out. Each version contains:

- A Vectorized Body—using packed AVX instructions.
- A Remainder Loop—added to compensate for the Trip Count not being a multiple of the Vector Length.
- A Peel Loop—this is a consequence of the array being referenced by `startpos` not being aligned correctly for AVX.

Twelve loops in total. In our case, the Peeled Loops are responsible for almost 60% of the total loops runtime, with the Vectorized Body taking just over 30%, leaving the Remainder Loops to consume 10%. Thus over 40% of the time is spent outside the Vectorized Body—this is something that needs investigation by analogy with the investigation we’ve undertaken in the previous section.

![](img/16cb41208935c5f22dd1044f03f2e31b_501_0.png)

**FIGURE 23.11** Analysis results of the loop in fGetOneMassSite. Alignment and padding advice given by Advisor Recommendations.

In the Recommendation section (the lower part of Figure 23.11), there are two problems in the `fGetOneMassSite` function that need fixing:

- The alignment of the array pointed to by `startpos`.
- The Trip Count and data padding.

### Fixing the problem

In our code, the real problem is that the compiler was not certain if the array pointed to by `startpos` is aligned, and therefore assumes it is unaligned. To fix this, we simply use a pragma to tell the compiler the data are aligned:

```cpp
#pragma vector aligned
```

In any codes that you work on, you must be certain that the array is actually aligned before using this pragma, otherwise your program may fail. If you need more help on getting your data aligned, you can go to one of the URLs in section “For more information”. You can also confirm the alignment of your data at runtime using Advisor’s Memory Access Pattern (MAP) tool, but this topic is out of scope for this chapter.

After dealing with alignment, we still need to fix the loop count (and remainder-driven overhead) issue. To do that, we repeat the padding steps done in the last loop, and also tell the compiler that the trip count is 20 via `#pragma loop count`. The code in Figure 23.12 shows the modified loop.

```cpp
double fGetOneMassSite(double* startpos)
{
    double mass=0.0;
    double *pt1;
    pt1= startpos;

    #pragma loop count (20)
    #pragma vector aligned
    for(int i=0; i< lbsy.nq + 1; i++) {
        mass += *pt1;
        pt1 ++;
    }
    pt1--;
    mass -= *pt1;
    pt1 = NULL;
    return mass;
}
```

**FIGURE 23.12** Code listing—calculating the mass density.

## BALANCING OVERHEADS AND OPTIMIZATION TRADE-OFFS

The padding technique that we used for the first two loops has both performance and code maintenance costs.

- From a **performance** perspective, by padding we avoid overhead in the scalar part, but we introduce extra computations in the vector part.
- From a **code maintenance** perspective, we have to rework data structure allocations and potentially introduce workload-dependent pragma definitions.

Fortunately, in our case, the performance benefit outweighs any performance loss, and the code maintenance burden is light.

In our example, the loop trip count values are defined by number of velocities, which in our available data sets are limited to the values 15, 19, and 27 (according to lattices DnQm taxonomy). This means that the number of extra “padding” iterations needed in the loop remainder is always +1 for AVX/AVX2 platforms.

For future AVX-512 and current IMCI platforms, the D3Q15 data set should benefit from the doubling of the Vector Length on Intel Xeon Phi coprocessors, but D3Q19 and D3Q27 (due to wider VL) will be less optimal.

From a code maintenance perspective, the earlier suggestion of replacing `nq_full_width` with *trip count + VL − (trip count mod VL)* can be used to avoid hardcoding the number of padding iterations and loop counts. The pragma hardcoding (Figures 23.8 and 23.12) could either be addressed by using a more flexible pragma loop count *min, max, avg* clause or by using code parameterization techniques like C pre-processor conditionalization, C++ template specialization or by using C++11 functors.

## OPTIMIZING THE MOVE PARTICLES TO NEIGHBORING GRID LOOP (lbpSUB.cpp:1247)

In this section, we deal with the loop in function `fPropagationSwap`, which is the loop that is also our number one hotspot. After doing a Dependency Analysis to confirm there are no dependencies, we vectorize the original scalar loop and then run a Memory Access Pattern analysis to find out why the loop is performing so badly. We then improve the performance by applying OpenMP 4.0 standard `#pragma simd` directives at a different loop nest level.

### The loop in function fPropagationSwap

This loop moves particles to neighboring grid points using a swap algorithm. This is the last of the loops we shall look at in this chapter. The code consists of a five-level nested loop within the function `fPropagationSwap`. At the deepest level, particles are swapped to their neighbors using the function `fSwapPair`—see Figure 23.13.

We already know from Section “Analyzing the Lattice Boltzmann code” that the loop at `lbpSUB.cpp:1247` often takes more time than any other loop. Additionally (Figure 23.14), we can see that the loop:
