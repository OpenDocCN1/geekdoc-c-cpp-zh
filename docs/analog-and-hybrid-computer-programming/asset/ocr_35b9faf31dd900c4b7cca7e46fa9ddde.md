# Table 5.2. Clock control of a sample and hold circuit

| Cycle | Group I | Group I | Group II | Group II |
| | IC | HLT | IC | HLT |
| 0 | ✓ |  |  |  |
| 1 |  | ✓ |  |  |
| 2 |  |  | ✓ |  |
| 3 |  |  |  | ✓ |
| 4 | ✓ |  |  |  |
| 5 |  | ✓ |  |  |
| ... | ... | ... | ... | ... |

# Fig. 5.38. Basic sample and hold circuit

![](bbox=[0.1, 0.38, 0.95, 0.6])

right with the delay time T depending on the clock frequency and the number of double integrator stages. Circuits like these have been used extensively to implement sampled data systems and difference equations⁵⁹ but they are not directly suitable to implement a highly granular delay circuit due to the staggering number of integrators that would be required.

A more suitable implementation of such an integrator chain is called a bucket brigade device, BBD for short. This name is quite descriptive as they are implemented by a number of capacitors connected as shown in figure 5.39.⁶⁰ These capacitors are interconnected by field effect transistors (FETs), which are controlled by a two-phase clock signal, CP1 and CP2, controlling the odd and even numbered FETs respectively. A voltage applied to the input IN is stored in the first capacitor of the bucket brigade by a clock pulse on CP2. This pulse is followed by a pulse on CP1 which transfers this value from the first capacitor to the second and so on. Since the number of capacitor stages is fixed⁶¹ the desired delay is achieved by adjusting the frequency of i the two-phase clock signal.⁶²