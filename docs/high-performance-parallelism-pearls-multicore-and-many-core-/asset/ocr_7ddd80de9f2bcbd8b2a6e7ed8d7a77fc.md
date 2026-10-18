```
Compute the column index globalCol of the stripe in the
alignment matrix;
Compute the starting index startIndex of the GV buffer
for the stripe;
for (i=16; i < numTileCols; ++i, ++globalCol) {
    vHUp = _mm512_set1_epi32(GH[globalCol].h);
    vEUp = _mm512_set1_epi32(GH[globalCol].e);
    vWUp = _mm512_alignr_epi32(vF, vHUp, 15);
    vHUp = _mm512_alignr_epi32(vH, vHUp, 15);
    vE = _mm512_sub_epi32(vEUp,vGapExtend);
    vTmp = _mm512_sub_epi32(vHUp,vGapOE);
    vE = _mm512_max_epi32(vE,vTmp);
    vF = _mm512_sub_epi32(vF,vGapExtend);
    vTmp = _mm512_sub_epi32(vH,vGapOE);
    vF = _mm512_max_epi32(vF,vTmp);
    Compute the substitution score vSubScore;
    vH = _mm512_add_epi32(vHDiag, vSubScore);
    vTmp = _mm512_max_epi32(vE,vF);
    vH = _mm512_max_epi32(vH,vZero);
    vH = _mm512_max_epi32(vH,vTmp);
    lmaxScore = _mm512_max_epi32(lmaxScore,vH);
    vHDiag = vHUp;
    Save the H and E values for the cell on the last
    row of the stripe
}
Save the H and F values for the cell on the last column
of the stripe;
```

# FIGURE 4.5

Kernel for the vectorized computation of Step 2 (refer to function _swKernelShared() in AlignCoreTiling.cpp).

# PARALLELIZATION ACROSS MULTIPLE COPROCESSORS USING MPI

Our distributed parallelization on a cluster of coprocessors is designed based on the MPI offload model, which launches MPI processes solely on the host CPUs and utilizes the offload capability within the process to offload some workload to the corresponding coprocessor. In this model, communications between coprocessors must be explicitly managed by the host via offload directives. The core idea of the distributed approach across multiple Intel Xeon Phi coprocessors is based on a second-level tiling. We further partition the alignment matrix into even bigger blocks of size αₘₚᵢ × βₘₚᵢ, reorganizing the matrix to have Rₘₚᵢ = ⌈m/αₘₚᵢ⌉ rows and Cₘₚᵢ = ⌈n/βₘₚᵢ⌉ columns (see Figure 4.6).

We call the corresponding diagonals block diagonals. All blocks within such a diagonal are distributed over a network of coprocessors and one block is assigned to one coprocessor. Within any block, a variant of the aforementioned tiled approach is employed on a single coprocessor, which additionally processes intermediate data computed by other MPI processes. Similar to the tiled approach, the