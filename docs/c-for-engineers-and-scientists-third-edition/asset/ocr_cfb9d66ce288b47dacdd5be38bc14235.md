# 34 Preliminaries

The introduction of transistors in the 1960s reduced the size and cost of computer hardware. The transistor's small size—about one-twentieth the size of vacuum tubes—allowed manufacturers to combine the ALU with the control unit into a single unit called the central processing unit (CPU). Combining the ALU and control unit made sense because control signals that a program generates are directed to the ALU in response to arithmetic logic instructions in the program. Combining the ALU with the control unit simplified the interface between these two units and improved speed.

Integrated circuits (ICs) were introduced in the 1960s, which resulted in another major reduction in the size required to produce a CPU. Initially, ICs were manufactured with up to 100 transistors on a single square-centimeter chip of silicon and were small-scale integrated (SSI) circuits. Current versions of these chips, called very large-scale integrated (VLSI) chips, can contain more than a million transistors. With VLSI technology, the giant computers of the 1950s could be transformed into today's and notebook PCs. Each unit required to form a computer (CPU, memory, and I/O) is manufactured on a single VLSI chip, and a single-chip CPU is referred to as a microprocessor. Figure 1.15 illustrates how these chips are connected internally in current desktop PCs.

![](bbox=[0.243, 0.442, 0.755, 0.558])

Figure 1.15 VLSI chip connections for a desktop PC

Concurrent with the remarkable reduction in hardware size has been a dramatic decrease in cost and increase in processing speeds. Computer hardware that cost more than a million dollars in 1950 could be purchased for less than $100. If the same reductions occurred in the automobile industry, for example, a Rolls Royce could be purchased for $10! Similarly, current predecessors' processing speeds have increased by a factor of thousands over their 1950s, with computational speeds now being measured in millions of instructions per second (MIPS) and billions of instructions per second (BIPS).

# Computer Storage

The physical components used in manufacturing a computer use the same symbols people use for numbers and letters. For example, the number 126 is not stored with the symbols 1, 2, and 6, nor is the letter you recognize as an A stored with this symbol. In this section, you see why and how computers store numbers. In Chapter 2, you see how letters are stored.