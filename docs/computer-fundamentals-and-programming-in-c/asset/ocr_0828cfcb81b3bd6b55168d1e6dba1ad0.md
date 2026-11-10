# 3.12 UNIVERSALITY OF NAND AND NOR GATES

NAND and NOR are called universal gates since the AND, OR, and NOT gates can be constructed with either of them.

It is possible to implement *any* logic expression using only NAND gates. This is because NAND gates, in the proper combination, can be used to perform each of the Boolean operations OR, AND, and NOT. Figure 3.12 shows how NAND gates are used to implement AND, OR, and NOT operations. Similarly, Fig. 3.13 depicts how NOR gates are used to implement AND, OR, and NOT operations.

![](bbox=[0.05, 0.26, 0.48, 0.43])

Fig. 3.12 NAND gates performing OR, AND, and NOT operations

![](bbox=[0.05, 0.49, 0.48, 0.67])

Fig. 3.13 NOR gates performing NOT, OR, and AND operations

# Note

+   - The NAND and NOR gates can not only be used to implement the AND, OR and NOT gate functions but can also implement any complex Boolean function.

# Check Your Progress

+   1. The NAND gate output will be low if the two inputs are
+   (a) 00      (b) 01
+   (c) 10      (d) 11
+   Answer: (d)

+   2. When an input signal A = 11001 is applied to a NOT gate serially, its output signal is
+   (a) 00111   (b) 00110
+   (c) 10101   (d) 11001
+   Answer: (b)

+   3. Write the expression for Boolean function:
+   F (A, B, C) = Σm(1, 4, 5, 6, 7) in standard POS form.
+   Answer: F = (A + B + C)(A + \bar{B} + C)(A + \bar{B} + \bar{C})

+   4. A universal logic gate is one, which can be used to generate any logic function. Which of the following is a universal logic gate?
+   (a) OR      (b) AND
+   (c) XOR     (d) NAND
+   Answer: (d)

+   5. The "maxterm form" of a Boolean function is
+   F(A,B,C,D) = ΣM(1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15). The equivalent "minterm form" of this function is
+   (a) Σm(0)   (b) ABCD
+   (c) ABC     (d) \bar{A}\bar{B}\bar{C}\bar{D}
+   Answer: (a)

# SUMMARY

A variable which can either be 'true' or 'false' is a logic variable. The basic operations of Boolean algebra are AND, OR, and NOT. The operations like AND, OR, Complementaion, Associative, Distributive, and Commutative have evolved from these. The property of duality and De Morgan's theorems has also been derived from the basic boolean operations. Simplification of Boolean expressions can be performed with the help of the above laws and theorems. Boolean expressions or functions can be represented using truth tables, minterms, or maxterms.

The inputs and outputs of logic gates have two discrete voltage values. The AND gate is a circuit built with electronic devices which gives a 'true' output only if all inputs are 'true'. The OR gate, which is constructed with electronic devices, gives a 'true' output if any input is 'true'. In the NOT gate, whatever input is applied, the opposite logic state appears at the output, e.g., for a 'true' input, the output is 'false' and vice versa. The NAND gate is equivalent to NOT-AND and the NOR gate to NOT-OR. XOR gate is similar to OR gate with the exception that when both inputs are 1, the output is 0. The XNOR gate, also known as coincidence gate, gives 1 as output only if both inputs are 0 or if both inputs are 1. Any boolean expression can be implemented with logic gates as the building blocks. NAND and NOR are universal gates as these can be used to construct the basic logic gates.