corresponding to the number of scalars that can fit into a SIMD register. This step is followed by loop distribution, which generates a sequence of loops replaced with the vector instructions, as follows:

```
```
// intermediate step after stripmining and Loop distribution
for (i = 0; i < 512; i+=4) {
    For (j = 0; j < 4; j++) vA[j] = A[i+j];
    For (j = 0; j < 4; j++) vB[j] = B[i+j];
    For (j = 0; j < 4; j++) vC[j] = C[i+j];
    For (j = 0; j < 4; j++) vD[j] = D[i+j];
    For (j = 0; j < 4; j++) vE[j] = vA[j]+vB[j];
    For (j = 0; j < 4; j++) vF[j] = vC[j]+vD[j];
    For (j = 0; j < 4; j++) D[i+j] = vD[j];
}
```
```

The block-level technique, on the other hand, is a more general technique focused on vectorizing basic block statements. As such, it relies on unrolling the innermost loop body by a factor corresponding to the vector register size (the same factor used in stripmining with the loop-level technique), packing all scalar instructions performing the same operation into vector instructions if dependences are not violated.

```
```
// intermediate step after unrolling and before packing
for (i = 0; i < 512; i+=4) {
    vA0 = vld(&A[i+0]);
    vA1 = vld(&A[i+1]);
    vB0 = vld(&B[i+0]);
    vB1 = vld(&B[i+1]);
    vC0 = vld(&C[i+0]);
    vC1 = vld(&C[i+1]);
    vD0 = vld(&D[i+0]);
    vD1 = vld(&D[i+1]);
    vt0 = vadd(vA0, vB0);
    vt1 = vadd(vA1, vB1);
    vt2 = vadd(vC0, vD0);
    vt3 = vadd(vC1, vD1);
    vst(&D[i+0], vt0);
    vst(&D[i+1], vt1);
    vst(&D[i+2], vt2);
    vst(&D[i+3], vt3);
}
```
```

The use of both techniques generates the following vectorized code:

```
```
for (i = 0; i < 512; i+=4) {
    vA = vld(&A[i]); // vector load
    vB = vld(&B[i]);
    vC = vld(&C[i]);
    vt = vmul(vA, vC); // vector mult
    vt = vadd(vt, vF); // vector add
    vst(&D[i], vtD); // vector store
}
```
```

# RESTRICT KEYWORD

The restrict keyword is part of the C programming language introduced in the C99 standard. This keyword is used when declaring pointers to convey to compilers that these pointers do not address memory regions that overlap with regions addressed by other pointers and are