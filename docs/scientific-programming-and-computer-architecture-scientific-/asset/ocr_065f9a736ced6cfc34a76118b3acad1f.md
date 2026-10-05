# 3.3. Optimizing the instruction pipeline

mulpd in the same cycle. There is no register read stall, and after suitable unrolling, the number of cycles per iteration is only slightly greater than 5.

# Peak performance without loads or stores

The loop body of the following program issues five addpd instructions and five mulpd instructions.

```
for(long i=0; i < nitns; i++){
    addxmm("%xmm0", "%xmm1");
    mulxm("%xmm1", "%xmm2");
    addxmm("%xmm3", "%xmm4");
    mulxm("%xmm4", "%xmm5");
    addxmm("%xmm6", "%xmm7");
    mulxm("%xmm7", "%xmm8");
    addxmm("%xmm9", "%xmm10");
    mulxm("%xmm10", "%xmm11");
    addxmm("%xmm12", "%xmm13");
    mulxm("%xmm13", "%xmm14");
}
```

The source operand of each mulpd is the destination operand of the add above. The hope is that this source operand is read directly from ROB, relieving pressure on the register ports. If that hope bears out, we should observe 5 cycles per iteration.

If the loop is unrolled 10 times, we observe 5.3 cycles per iteration in line with expectation. Some operands are indeed being read from ROB instead of the register file.

If the loop is not unrolled, it takes 7 cycles per iteration. Why does unrolling help? The assembly code for the loop includes an instruction to increment the loop counter i, which is stored in a register as %rax. It includes another instruction to compare the loop counter with nitns. The variable nitns is stored in a register. These instructions create additional pressure on the register ports. An overhead of 2 cycles is unreasonable. With unrolling, the overhead is amortized.

On a more modern AVX2/Haswell machine, the same program takes 5.8 cycles per iteration, even with unrolling. Evidently this program interacts with the