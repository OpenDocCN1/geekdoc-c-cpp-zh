
# Chapter 3. The Processor

| ISA | Year | Family | Registers | Instructions |
|---|---|---|---|--|
| SSE | 1999 | Pentium | XMM (128 bit) | ADDPS, MULPS |
| SSE2 | 2001 | Pentium 4, Nehalem, Westmere, Opteron, Ath | XMM (128 bit) | ADDDP, MULDP |
| AVX | 2011 | Sandy Bridge, Bulldozer, Jaguar | YMM (256 bit) | VADDDP, VMULPD, |
| AVX2 | 2013 | Haswell, Broadwell | YMM (256 bit) | VADDDP, VMULPD, VFMADDDP |
| AVX-512 | 2015 | Skylake | ZMM (512 bit) | VADDDP, VMULPD, VFMADDDP |

Table 3.1: Generations of x86 instruction set architectures (ISAs) and machines implementing them. The machine families typically include several machines. For example, Xeon-5650 and Xeon-5670 are machines in the Westmere family (or microarchitecture). This table was prepared by consulting several Wikipedia pages. For a list of machines used in this book, see table A.1 in the appendix. Not all versions of Skylake support AVX-512.

namely fmmadd132pd, fmmadd213pd, and fmmadd231pd. These instructions implement operations of the form c = c + ab or a = c + ab while operating on three vector registers. Thus, a fmmadd instruction applied to three YMM registers results in four additions and four multiplications.

We refer to machines as 2.6 GHz SSE2 or 3.6 GHz AVX2. The full information about the machine may be found by looking up table A.1 in the appendix. The instruction set is the part of the computer's architecture most pertinent to program speed, which explains the nomenclature we adopt.

The type of processor design we see today is a product of research that happened as early as the 1960s, with important additions in the 1970s and 1980s.³ These design

> ³See Hennessy and Patterson (1990-2011). The 1960s reference is to Tomasulo’s algorithm, which principles were incorporated into the x86 line in the 1990s, and the underlying design principles have not changed greatly since. The x86 instruction set has evolved gradually and methodically. Therefore, not only do the fundamental concepts of optimization for processor architectures remain the same, the particular form they take within C/C++ programs do not change much either.

In addition, there has been a great deal of convergence in processor technology since 2000 that nearly 100% of desktop processors are now x86. The pertinence of the particular examples, as well as of general principles of program optimization described in this chapter, is unlikely to diminish anytime. In fact, the pertinence of computer architecture to program optimization appears to be growing.

Section 3.3 shows how to optimize for the instruction pipeline for SSE2 machines. The instruction pipeline depends on the instruction set architecture and to a far lesser on its microarchitectural realization (family in table 3.1). Because the programs in this section are in assembly, they will need to be updated for machines with YMM and ZMM registers (AVX, AV2, AVX-512). The updating of the YMM registers is the topic of several exercises. Using XMM registers on the Xeon Phi has the advantage that the programs we discuss run on almost any computer, including AVX and AV2 machines.

The payoff from this type of optimization is increasing rapidly. A matrix multiplication program written in 2010 in C/C++ approached nearly a third of the speed of a program optimized for the SSE2 processor. Five years later, the C/C++ program does not even come within a tenth of the speed of a program optimized for the AVX2 processor pipeline.

In section 3.2.5, we explain why the same C/C++ program has become so much worse, when compared to a fully optimized program, over a span of five years. There are two related reasons. After clock speeds flated around 2003, and even before, processors have used greater and greater numbers of transistors for greater and greater parallelism. At one level, that translates to more and more processor cores in a single processor package. Inside a processor, same trend trends to vector registers and instruction pipelines that can simultaneously execute multiple instructions. Even as there is a greater pay-off in optimizing for such pipelines, it becomes harder for the compilers to do so.

## 3.1. Overview of the x86 architecture

In 2015, 100% of non-mobile computers and laptops run on x86 processors. It would take a cataclysmic event (cataclysmic for Intel Corporation), such as Apple Computers switching its MacBooks and desktops from the x86 line to ARM, for the x86 line to be truly challenged.^4 Intel is not vulnerable to market forces as it used to be or two decades ago, but it still dominates the processor benchmarks overwhelmingly. Such a cataclysmic event is not on the horizon as of 2015.

This section is a basic introduction to the x86 instruction architecture, which has dominated since its introduction in 1978. We look at registers and a little bit of assembly programming. Our intention is to lay the foundation for the next section. The following are some of the registers in the 64-bit x86 architecture:

-   - Eight 64-bit registers, including %rax, %rbx, %rcx, %rdx, %rdi, %rbp, %rsp.
-   If the r in the names above is replaced by e, we get names for 32-bit registers. These are the lower halves of the 64-bit registers.
-   Eight more 64-bit general-purpose registers %r8 through %r15.
-   To access only the lower 32 bits, we can use %r8d through %r15d. Here d stands for double word.
-   Floating point register stack with 80-bit registers called %st(0) through %st(7). Eight 64-bit MMX registers %mm0 through %mm7. We will never use these registers.

## Registers

The x86 64-bit architecture is first of all a specification of registers (see figure 3.2). The architecture was first introduced by AMD and later adopted by Intel. Some

To add two numbers in memory, for instance, typically we have to first move one or both of them to registers, add the two registers, and move the result from a register to a memory location. The addresses of the memory can also be held in the registers. When we write programs, all operands may be registers. When arithmetic operations are executed by the processor, all may be registers. Registers are very special because they are wired to circuits for carrying out arithmetic and logical operations. Variable names may only correspond to specific registers. The following are some of the registers in the 64-bit x86 architecture: (see listed above)
