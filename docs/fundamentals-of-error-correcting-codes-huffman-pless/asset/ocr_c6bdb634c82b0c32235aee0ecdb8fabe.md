![](bbox=[0.14, 0.09, 0.83, 0.28])

Figure 4.2 Encoder for $\mathcal{C}$, where $\mathcal{C}^{\perp} = (1 + x^2 + x^3)$. 

adder takes all its input signals and adds them in binary; this process is considered to occur instantaneously.

**Example 4.2.10** In Figure 4.2, we construct a linear feedback shift-register for encoding the [7, 3] binary cyclic code $\mathcal{C}$ with generator polynomial $g(x) = 1 + x + x^2 + x^4$. Then $g^{\perp}(x) = 1 + x^2 + x^3$, and so the parity check equations from (4.2) are:
$c_0 + c_2 = c_3,$
$c_1 + c_3 = c_4,$
$c_2 + c_4 = c_5,$
$c_3 + c_5 = c_6.$

The shift-register has three flip-flops. Suppose we input $c_0 = 1$, $c_1 = 0$, and $c_2 = 0$ into the shift-register. Initially, before the first clock cycle, the shift-register has three unknown quantities, which we can denote by ***. The switch is set at position A for three clock cycles, in which case the digits 1, 0, 0 from the source are moved into the shift-register from left to right, as indicated in Table 4.1. These three bits also move to the transmission channel. Between clock cycles 3 and 4, the switch is set to position B, which enables the

**Table 4.1 Shift-register for** $\mathcal{C}$**, where** $\mathcal{C}^{\perp} = (1 + x^2 + x^3)$ **with input 100**

| Clock cycle | Switch | Source | Channel | Register |
|---|---|---|---|---|
| 1 | A | 1 | 1 | 1** |
| 2 | A | 0 | 0 | 01* |
| 3 | A | 0 | 0 | 001 |
| 4 | B | | 1 | 100 |
| 5 | B | | 1 | 110 |
| 6 | B | | 1 | 111 |
| 7 | B | | 0 | 011 |