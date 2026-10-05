
-   Sixteen 128-bit registers %xmm0 through %xmm15. Each register can hold two double-precision numbers. These are the so-called SSE registers.

-   Each XMM register is extended to a 256-bit YMM register in AVX (see table 3.1). The YMM registers are %ymm0 through %ymm15. The YMM registers have been extended in AVX-512 (see table 3.1).

The AMD/Intel manuals use slightly different names for the registers. For instance, %rax becomes RAX. The names in our list anticipate use of GAS (the GNU assembler). The partial list omits a number of registers. From some of the registers we have listed, we get 16-bit or word-length registers and 8-bit or byte-length integers by changing the names appropriately.

This list of registers may appear long and a bit intimidating. To master all can indeed be a task. For our purposes, it suffices to know that there are 16 general-purpose registers and 16 XMM/YMM registers. The different uses that these registers are put to emerge as this chapter progresses. The XMM/YMM registers are the basis of scientific programs.

There is a 64-bit register called %rip that users normally do not access. That register is the instruction pointer. It is the offset of the address of the next instruction to be executed relative to some base. But that interpretation can be problematic because of instruction pipelining and out-of-order execution.

# Backward binary compatibility

The 64-bit x86 architecture carries within it ghosts from decades past. Some of these ghosts are easily seen in the naming of the register set, which is the most basic feature of processor architectures. At first there seems to be no good reason to call a register rax or rbx. However, when the first 8086 16-bit processor was introduced back in 1978, large numbers of registers must have seemed a distant dream. So it was natural to use the first few letters of the alphabet for the registers. When the 32-bit 80386 was introduced in 1985, names such as ax were changed to eax, signaling the enhancements to the size of the registers. The register names in the 64-bit x86 architecture reflect this evolution.

Binary compatibility is the reason for this peculiar evolution. It may make no sense to expect a 64-bit x86 processor of today to run a 16-bit binary from 1978, but it makes sense to expect it to run the 32-bit binaries of a few years ago. All the 64-bit x86 processors have a 32-bit mode that can be turned on by the operating system. If they did not have such a mode, nearly every one of the 32-bit software systems available would have failed when the 64-bit architecture was first introduced. Backward binary compatibility gives software developers, especially developers of operating systems, to catch up. Backward compatibility means that an instruction such as MOAX EBX that made sense in the 32-bit architecture must also make sense in the 64-bit x86 architecture. Not only that, its encoding in bits must be exactly 89 C3 in hexadecimal—the first byte is the opcode for MOVL and the second byte, which encodes the source and destination registers, is the so-called ModR/M byte.

The disadvantage of backward binary compatibility is that it constraints the design of the instruction set and the microarchitecture used to implement it in hardware. Every time the instruction set is extended, the binary encoding of the earlier instruction as well as its semantics must be preserved. This burden can be considerable. For instance, programs written in 1990 could rely on the register %eip to the address of the next instruction to be executed and manipulate that register to jump to some other point in the program. Not only today's x86 architecture include that register, it should also give the same effect when the %eip is altered to jump to some other location in the program. Having to bear this considerable burden means that the x86 architecture is infamous for its extremely complicated encodings of instructions.

History has shown that the disadvantages of backward binary compatibility are outweighed by the advantage of being readily usable. The x86 architecture always seeks to be usable. A new design that is brought out today must run yesterday's binaries. This emphasis on usability has made the vast majority of today's computers (including mobile devices) use x86 processors.

Yet one must not exaggerate the benefits of backward binary compatibility in relation to the x86 architecture. Intel, the foremost champion of the x86 line, is no longer the invincible behemoth it once was. Intel is tied to the PC business, which is in gradual decline, and has no control over hardware or software platforms in the rapidly growing mobile computing and networking sectors.

> ⁶⁷The ARM architecture has a much simpler instruction set and has achieved wide use on mobile gadgets. The number of ARM devices is greater than the number of x86 computers. Thus, the ARM architecture does not suffer from a lack of widespread adoption and the consequent lack of economy of scale, which has been a bane of previous challengers to x86. However, the terms of commercial licensing of ARM are such that the benefits of its wide adoption are shared by many companies.

Despite the enormous investment in design accumulated over many years, the volume of profit being generated in the computer business is now so great that a legitimate challenger to the x86 line is not inconceivable. In a business that is growing exponentially, what happens in the next five years can be...

## 3.1. Overview of the x86 architecture

The reader may find it a little puzzling that “double” (or “long”) is used for 32-bit operands and “quad” for 64-bit operands. A word in the original 8086 machine of 1978 was 16 bits. Thus, double words are 32 bits and quad words are 64 bits, as a result of a choice made long ago.

> The third byte is given by the AMD manuals.
