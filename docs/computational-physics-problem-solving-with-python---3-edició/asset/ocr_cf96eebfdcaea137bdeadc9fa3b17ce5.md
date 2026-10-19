# Table 10.1 Computation of c = (a + b)/(d × f).

| Arithmetic Unit | Step 1 | Step 2 | Step 3 | Step 4 |
|---|---|---|---|---|
| A1 | Fetch a | Fetch b | Add | — |
| A2 | Fetch d | Fetch f | Multiply | — |
| A3 | — | — | — | Divide |

# 10.4

# CPU Design: Reduced Instruction Set Processors

Reduced instruction set computer (RISC) architecture (also called superscalar) is a design philosophy for CPUs developed for high-performance computers and now used broadly. It increases the arithmetic speed of the CPU by decreasing the number of instructions the CPU must follow. To understand RISC, we contrast it with CISC (complex instruction set computer) architecture. In the late 1970s, processor designers began to take advantage of very-large-scale integration (VLSI), which allowed the placement of hundreds of thousands of elements on a single CPU chip. Much of the space on these early chips was dedicated to microcode programs written by chip designers and containing machine language instructions that set the operating characteristics of the computer. There were more than 1000 instructions available, and many were similar to higher level programming languages like Pascal and Forth. The price paid for the large number of complex instructions was slow speed, with a typical instruction taking more than 10 clock cycles. Furthermore, a 1975 study by Alexander and Wortman of the XLP compiler of the IBM System/360 showed that about 30 low-level instructions accounted for 99% of the use with only 10 of these instructions accounting for 80% of the use.

The RISC philosophy is to have just a small number of instructions available at the chip level, but to have the regular programmer’s high-level language, such as Fortran or C, translate them into efficient machine instructions for a particular computer’s architecture. This simpler scheme is cheaper to design and produce, lets the processor run faster, and uses the space saved on the chip by cutting down on microcode to increase arithmetic power. Specifically, RISC increases the number of internal CPU registers, thus, making it possible to obtain longer pipelines (cache) for the data flow, a significantly lower probability of memory conflict, and some instruction-level parallelism.

The theory behind this philosophy for RISC design is the simple equation describing the execution time of a program:

CPU time = number of instructions × cycles/instruction × cycle time .

(10.3)

Here “CPU time” is the time required by a program, “number of instructions” is the total number of machine-level instructions the program requires (sometimes called the path length), “cycles/instruction” is the number of CPU clock cycles