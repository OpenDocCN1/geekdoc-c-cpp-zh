# Chapter 3. The Processor

During every cycle, it is possible to read only three registers from the register file in the SSE2/Nehalem microarchitecture. Here the addpd would need to read two registers and mulpd would need to read two others. The initial answer is to point out that one of the two instructions cannot be dispatched because four registers cannot be read in the same cycle.

That is not a complete answer, however. After an instruction completes, it spends some time in the reorder buffer (ROB) (see figure 3.4) before it is retired. If an operand needed to dispatch an instruction can be captured directly as the output of an instruction that is waiting in ROB, there is no need to use a register port. In fact, in the earlier Core 2 or Merom microarchitecture, the program takes only 5 cycles per iteration, although the Core 2 microarchitecture provides only two ports to read from the register file. It appears that each addpd and mulpd instruction in the loop body captures the previous iteration from ROB on Core 2. The reason that SSE2/Nehalem does not read from ROB as Core 2 is is unknown.

Another confirmation that register stalls are responsible for slowing the program down to 8 cycles per iteration, instead of the expected 5, may be found by running the same program on an AVX/AVX2 machine. On more modern machines, there are more register ports, and therefore register stalls are not an issue. The program realizes 5 cycles per iteration.

Our second attempt is the following program:

```
for(i=0; i < nitsns; i++){
    addmm("%xmm8", "%xmm0");
    addmm("%xmm8", "%xmm1");
    addmm("%xmm8", "%xmm2");
    mulmm("%xmm8", "%xmm3");
    mulmm("%xmm8", "%xmm4");
    mulmm("%xmm8", "%xmm5");
    mulmm("%xmm8", "%xmm6");
    mulmm("%xmm8", "%xmm7");
}
```

In this program, each addpd and mulpd instruction uses %xmm8 as its source register. Only three registers need to be read from the register file to dispatch an addpd and