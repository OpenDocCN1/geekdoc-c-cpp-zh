
## 8.1 Issues in the Design of a Code Generator

further optimization. If the IR reflects some of the low-level details of the underlying machine, then the code generator can use this information to generate more efficient code sequences.

The nature of the instruction set of the target machine has a strong effect on the difficulty of instruction selection. For example, the uniformity and completeness of the instruction set are important factors. If the target machine does not support each data type in a uniform manner, then each exception to the general rule requires special handling. On some machines, for example, floating-point operations are done using separate registers.

Instruction speeds and machine idioms are other important factors. If we do not care about the efficiency of the target program, instruction selection is straightforward. For each type of three-address statement, we can design a code skeleton that defines the target code to be generated for that construct. For example, every three-address statement of the form `x = y + z`, where `x`, `y`, and `z` are statically allocated, can be translated into the code sequence

```
LD  R0, y       // R0 = y          (load y into register R0)
ADD R0, R0, z   // R0 = R0 + z      (add z to R0)
ST  x, R0       // x = R0           (store R0 into x)
```

This strategy often produces redundant loads and stores. For example, the sequence of three-address statements

```
a = b + c
d = a + e
```

would be translated into

```
LD  R0, b       // R0 = b
ADD R0, R0, c   // R0 = R0 + c
ST  a, R0       // a = R0
LD  R0, a       // R0 = a
ADD R0, R0, e   // R0 = R0 + e
ST  d, R0       // d = R0
```

Here, the fourth statement is redundant since it loads a value that has just been stored, and so is the third if `a` is not subsequently used.

The quality of the generated code is usually determined by its speed and size. On most machines, a given IR program can be implemented by many different code sequences, with significant cost differences between the different implementations. A naive translation of the intermediate code may therefore lead to correctly but unacceptably inefficient target code.

For example, if the target machine has an “increment” instruction (`INC`), then the three-address statement `a = a + 1` may be implemented more efficiently by the single instruction `INC a`, rather than by a more obvious sequence that loads `a` into a register, adds one to the register, and then stores the result back into `a`:

the problem by generating code for the three-address statements in the order in which they have been produced by the intermediate code generator. In Chapter 10, we shall study code scheduling for pipelined machines that can execute several operations in a single clock cycle.

## 8.2 The Target Language

Familiarity with the target machine and its instruction set is a prerequisite for designing a good code generator. Unfortunately, in a general discussion of code generation it is not possible to describe any target machine in sufficient detail to generate good code for a complete language on that machine. In this chapter, we shall use as a target language assembly code for a simple computer that is representative of many register machines. However, the code-generation techniques presented in this chapter can be used on many other classes of machines as well.

### 8.2.1 A Simple Target Machine Model

Our target computer models a three-address machine with load and store operations, computation operations, jump operations, and conditional jumps. The underlying computer is a byte-addressable machine with `n` general-purpose registers, `R0, R1, ..., R_{n-1}`. A full-fledged assembly language would have scores of instructions. To avoid hiding the concepts in a myriad of details, we shall use a very limited set of instructions and assume that all operands are integers. Most instructions consist of an operator, followed by a target, followed by a list of source operands. A label may precede an instruction. We assume the following kinds of instructions are available:

- **Load operations.** The instruction `LD dst, addr` loads the value in location `addr` into location `dst`. This instruction denotes the assignment `dst = addr`. The most common form of this instruction is `LD r, x`, which loads the value in location `x` into register `r`. An instruction of the form `LD r1, r2` is a *register-to-register copy* in which the contents of register `r2` are copied into register `r1`.

- **Store operations.** The instruction `ST x, r` stores the value in register `r` into the location `x`. This instruction denotes the assignment `x = r`.

- **Computation operations** of the form `OP dst, src1, src2`, where `OP` is an operator like `ADD` or `SUB`, and `dst`, `src1`, and `src2` are locations, not necessarily distinct. The effect of this machine instruction is to apply the operation represented by `OP` to the values in locations `src1` and `src2`, and place the result of this operation in location `dst`. For example, `SUB r1, r2, r3` computes `r1 = r2 - r3`. Any value formerly stored in `r1` is lost, but, if `r1` is `r2` or `r3`, the old value is read first. Unary operators that take only one operand do not have a `src2`.

- **Unconditional jumps:** The instruction `BR L` causes control to branch to the machine instruction with label `L`. (`BR` stands for *branch*.)

- **Conditional jumps** of the form `Bcond r, L`, where `r` is a register, `L` is a label, and `cond` stands for any of the common tests on values in the register `r`. For example, `BLTZ r, L` causes a jump to label `L` if the value in register `r` is less than zero, and allows control to pass to the next machine instruction if not.

We assume our target machine has a variety of addressing modes:

- In instructions, a location can be a variable name `x` referring to the memory location that is reserved for `x` (that is, the l-value of `x`).

- A location can also be an indexed address of the form `a(r)`, where `a` is a variable and `r` is a register. The memory location denoted by `a(r)` is computed by taking the l-value of `a` and adding it to the l-value in register `r`. For example, the instruction `LD R1, a(R2)` has the effect of setting `R1 = contents(a + contents(R2))`, where `contents(x)` denotes the contents of the register or memory location represented by `x`. This addressing mode is useful for accessing arrays, where `a` is the base address of the array (that is, the address of the first element), and `r` holds the number of bytes past that address we wish to go to reach one of the elements of array `a`.

- A memory location can be an integer indexed by a register. For example, `LD R1, 100(R2)` has the effect of setting `R1 = contents(100 + contents(R2))`, that is, of loading into `R1` the value in the memory location obtained by adding 100 to the contents of register `R2`. This feature is useful for following pointers, as we shall see in the example below.

- We also allow two indirect addressing modes: `*r` means the memory location found in the location represented by the contents of register `r`, and `*100(r)` means the memory location found in the location obtained by adding 100 to the contents of `r`. For example, `LD R1, *100(R2)` has the effect of setting `R1 = contents(contents(100 + contents(R2)))`, that is, of loading into `R1` the value in the memory location stored in the memory location obtained by adding 100 to the contents of register `R2`.

- Finally, we allow an immediate constant addressing mode. The constant is prefixed by `#`. The instruction `LD R1, #100` loads the integer 100 into register `R1`, and `ADD R1, R1, #100` adds the integer 100 into register `R1`.

Comments at the end of instructions are preceded by `//`.

**Example 8.2:** The three-address statement `x = y - z` can be implemented by the machine instructions:
