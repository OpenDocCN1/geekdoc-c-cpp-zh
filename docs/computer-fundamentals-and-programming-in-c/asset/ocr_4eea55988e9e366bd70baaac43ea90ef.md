**Table 3.9 Truth table for NOT gate**

| Inputs | Output |
| --- | --- |
| A | Y = \bar{A} |
| 0 | 1 |
| 1 | 0 |

The NOT gate in Fig. 3.3(b) uses a transistor. When the voltage applied to input A is zero volts, the transistor is reverse biased, so it is off. Hence the voltage at Y is +Vcc i.e., HIGH. But when A is +Vcc, the transistor is forward biased thereby driving the transistor to an on state or saturation. The voltage at Y = Vcc (sat), which is practically zero volts, i.e., Y is LOW. The truth table for this circuit is given in Table 3.10.

![](bbox=[0.03, 0.285, 0.46, 0.49])

**Table 3.10 Truth table for a NOT gate (Vcc = 5 V)**

| Inputs | Output |
| --- | --- |
| A | Y = \bar{A} |
| 0 V | 5 V |
| 5 V | 0 V |

# ### 3.9.4 NAND Gate

The NAND gate implements the NAND function, which means NOT-AND. The inputs are ANDed and then NOTed to get a single output. The output of NAND gate is HIGH if any or all of the inputs are LOW. When all inputs are HIGH, the output is LOW. Table 3.11 depicts the truth table for a two-input NAND gate.

**Table 3.11 Truth table for a two-input NAND gate**

| Inputs | | Output |
| --- | --- | --- |
| A | B | Y = \overline{AB} |
| 0 | 0 | 1 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |

In Fig. 3.4, the circle at the output of the NAND gate denotes the logical inversion, just as it did at the output of the inverter. Note that the output is the overbar of the ANDed input values. As shown in the figure, the NAND function can also be performed by a bubbled OR gate.

As with AND, there is no limit to the number of inputs that may be applied to a NAND function, so there is no functional limit to the number of inputs a NAND gate may have. However, for practical reasons, commercial NAND gates are most commonly manufactured with two, three, or four inputs to fit in a 14-pin or 16-pin IC package.

![](bbox=[0.5, 0.28, 0.98, 0.47])

# ### 3.9.5 NOR Gate

The NOR gate is an OR gate with inverted output. Whereas the OR gate allows the output to be HIGH (logic 1) if any one or more of its inputs are HIGH, the NOR gate inverts this and forces the output to logic 0 when any input is HIGH, i.e., the output of a NOR gate is LOW if any of the inputs are HIGH. The output is HIGH when all inputs are LOW. The truth table of a two-input NOR gate is given in Table 3.12.

The NOR function uses the plus sign (+) operator with the output represented by an expression with an overbar to indicate the OR inversion. In the logic diagram, shown in Fig. 3.5(b), the symbol designates the NOR gate. This is an OR gate with a circle to designate the inversion. The NOR function can also be performed by a bubbled AND gate, as depicted in Fig. 3.5(c).

The NOR function can have any number of inputs but only one output. As with other gates, practical commercial NOR gates are mostly limited to two, three, and four inputs to fit in standard IC packages.