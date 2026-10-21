| Color | Code | Zeros |
|---|---|---|
| Black | 0 | - |
| Brown | 1 | 0 |
| Red | 2 | 00 |
| Orange | 3 | 000 |
| Yellow | 4 | 0000 |
| Green | 5 | 00000 |
| Blue | 6 | 000000 |
| Violet | 7 | 0000000 |
| Gray | 8 | 00000000 |
| White | 9 | 000000000 |

Figure A.2: Resistor values are encoded using colors.

that is so small it fits on them. So, they use a trick and encode the value using colored stripes.

Usually you find four or five stripes on a resistor (at least on through-hole parts; SMD resistors don't have them). One of them is separated from the others by a gap (see Figure A.3, on the next page). The separate stripe is on the right side of the resistor, and it tells you about the resistor's accuracy. Gold stands for an accuracy of ±5 percent, silver for ±10 percent, and no stripe means ±20 percent. Using the remaining stripes, you can calculate the resistor value.

You read the stripes from left to right, and every color stands for a digit (see Figure A.2). The rightmost stripe—that is the third or fourth one—stands for an amount of zeros to be added to the preceding digits. In Figure A.3, on the next page, you can see three examples:

+   - On the first resistor we find four stripes: brown (1), green (5), brown (1 zero), silver (±10%). That means we have a resistor value of 150Ω.
+   - The second resistor has four stripes again: yellow (4), violet (7), orange (3 zeros), gold (± 5%). So, this resistor has a value of 47000Ω = 47k Ω.
+   - The third resistor has five stripes: brown (1), red (2), red (2), green (5 zeros), silver (±10%), so the value is 12,200,000Ω = 12.2MΩ.