```
// File: dslash.common.cc
void project(InstVector& ivector, string base, string offset, proj_ops& ops,
    bool isFace, string mask, int dir)
{
    string tmask("");
    PrefetchL1FullSpinorDirIn(ivector, base, offset, dir);

    for(int s = 0; s < 2; s++) {
        for(int c = 0; c < 3; c++) {
            LoadSpinorElement(ivector, psi[0][RE], base, offset, ops.s[s][0],
                c, RE, isFace, mask, dir);
            LoadSpinorElement(ivector, psi[0][IM], base, offset, ops.s[s][0],
                c, IM, isFace, mask, dir);
            LoadSpinorElement(ivector, psi[1][RE], base, offset, ops.s[s][1],
                c, RE, isFace, mask, dir);
            LoadSpinorElement(ivector, psi[1][IM], base, offset, ops.s[s][1],
                c, IM, isFace, mask, dir);

            ops.CVecFunc[s](ivector, b_spinor[s][c], psi[0], psi[1], /*mask*/
                tmask); // Not using mask here
        }
    }
}
```

# FIGURE 9.22

Generating L1 prefetches for the projection operation. We explicitly prefetch the whole spinor into L1, before element wise loading.

the caches of other cores than the one which needs them. Therefore, we allow the possibility of prefetching up to four neighboring spinors. For each of these we supply a pointer and an offset. The base pointers are xyBase (current tile), pfBase2, pfBase3, and pfBase4. The prefetch offsets to these pointers are siprefdist1, siprefdist2, and so on up to siprefdist4. We also prefetch gauge fields with offset gprefdist from the current gBase and can prefetch the next output spinor with base outBase. Some of these are commented out or not used in the implementation, but that is the basic idea.

The base pointers and siprefdist offsets are calculated during the lattice traversal loop in functions like DyzPlus in the QPhiX library. In Figure 9.18, we have hidden these computations for clarity, but they can certainly be found in the attached code bundle.

When the code generation is run, the L2 prefetches are generated into a separate instruction vector from the mainline code, and are merged with the main Dslash code just before serializing to try and space them evenly through the generated code. This merging is done by the function mergeVectorWithL2Prefetches in the source file dslash.cc

# GENERATING THE CODE

Now that we have covered the mechanics, let us generate the code. To do this we need to look at two makefiles. One is the main Makefile. Here our main work is to choose the architecture by editing the variable mode in the first line. Right now, it is set to mic which is fine for Intel Xeon Phi coprocessors. We can also set it to, for example, avx for AVX code, or scalar for nonvectorized code.

Second, for each supported mode there is a file called customMake.xxx, where xxx is the mode. We can look, for example, at customMake.mic. In this file, we can set a variety of options for code generation, for example, whether to use streaming stores, or whether we should use L1, L2 prefetching, etc. We show a snippet of customMake.mic in Figure 9.23 where we enabled all the prefetching options and