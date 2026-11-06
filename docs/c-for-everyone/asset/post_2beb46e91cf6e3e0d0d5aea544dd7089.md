
### P3.24

Write a program that asks the user to enter a month (1 for January, 2 for February, and so on) and then prints the number of days in the month. For February, print “28 or 29 days”.

```text
Enter a month: 5
30 days
```

Do not use a separate if/else branch for each month. Use Boolean operators.

### P3.25

A year with 366 days is called a leap year. A year is a leap year if it is divisible by four (for example, 1980), except that it is not a leap year if it is divisible by 100 (for example, 1900); however, it is a leap year if it is divisible by 400 (for example, 2000). There were no exceptions before the introduction of the Gregorian calendar on October 15, 1582 (1500 was a leap year). Write a program that asks the user for a year and computes whether that year is a leap year.

### P3.26

Add error handling to Exercise P3.2. If the user does not enter a number when expected, or provides an invalid unit for the altitude, print an error message and end the program.

### Engineering P3.27

Write a program that prompts the user for a wavelength value and prints a description of the corresponding part of the electromagnetic spectrum, as given in Table 7.

![](img/5e58fb4c840712efd6ed6fa82bb97f57_150_0.png)

**Table 7 Electromagnetic Spectrum**

| Type | Wavelength (m) | Frequency (Hz) |
|---|---|---|
| Radio Waves | > 10⁻¹ | < 3 × 10⁹ |
| Microwaves | 10⁻³ to 10⁻¹ | 3 × 10⁹ to 3 × 10¹¹ |
| Infrared | 7 × 10⁻⁷ to 10⁻³ | 3 × 10¹¹ to 4 × 10¹⁴ |
| Visible light | 4 × 10⁻⁷ to 7 × 10⁻⁷ | 4 × 10¹⁴ to 7.5 × 10¹⁴ |
| Ultraviolet | 10⁻⁸ to 4 × 10⁻⁷ | 7.5 × 10¹⁴ to 3 × 10¹⁶ |
| X-rays | 10⁻¹¹ to 10⁻⁸ | 3 × 10¹⁶ to 3 × 10¹⁹ |
| Gamma rays | < 10⁻¹¹ | > 3 × 10¹⁹ |

### Engineering P3.28

Repeat Exercise P3.27, modifying the program so that it prompts for the frequency instead.

### Engineering P3.29

Repeat Exercise P3.27, modifying the program so that it first asks the user whether the input will be a wavelength or a frequency.

### Engineering P3.30

A minivan has two sliding doors. Each door can be opened by either a dashboard switch, its inside handle, or its outside handle. However, the inside handles do not work if a child lock switch is activated. In order for the sliding doors to open, the gear shift must be in *park*, and the master unlock switch must be activated. (This book’s author is the long-suffering owner of just such a vehicle.)

![](img/5e58fb4c840712efd6ed6fa82bb97f57_150_1.png)

Your task is to simulate a portion of the control software for the vehicle. The input is a sequence of values for the switches and the gear shift, in the following order:

- Dashboard switches for left and right sliding door, child lock, and master unlock (0 for off or 1 for activated)
- Inside and outside handles on the left and right sliding doors (0 or 1)
- The gear shift setting (one of P N D 1 2 3 R).

A typical input would be `0 0 0 1 0 1 0 0 P`.
Print “left door opens” and/or “right door opens” as appropriate. If neither door opens, print “both doors stay closed”.

### Engineering P3.31

Sound level L in units of decibel (dB) is determined by

$$L = 20\log_{10}(p/p_0)$$

where p is the sound pressure of the sound (in Pascals, abbreviated Pa), and p₀ is a reference sound pressure equal to 20 × 10⁻⁶ Pa (where L is 0 dB). The following table gives descriptions for certain sound levels.

![](img/5e58fb4c840712efd6ed6fa82bb97f57_151_0.png)

| Sound level | Decibels |
|---|---:|
| Threshold of pain | 130 dB |
| Possible hearing damage | 120 dB |
| Jackhammer at 1 m | 100 dB |
| Traffic on a busy roadway at 10 m | 90 dB |
| Normal conversation | 60 dB |
| Calm library | 30 dB |
| Light leaf rustling | 0 dB |

Write a program that reads a value and a unit, either dB or Pa, and then prints the closest description from the list above.

### Engineering P3.32

The electric circuit shown below is designed to measure the temperature of the gas in a chamber.

![](img/5e58fb4c840712efd6ed6fa82bb97f57_151_1.png)

The resistor R represents a temperature sensor enclosed in the chamber. The resistance R, in Ω, is related to the temperature T, in °C, by the equation

$$R = R_0 + kT$$

In this device, assume R₀ = 100 Ω and k = 0.5. The voltmeter displays the value of the voltage, Vₘ, across the sensor. This voltage Vₘ indicates the temperature, T, of the gas according to the equation

$$T = \frac{R}{k} - \frac{R_0}{k} = \frac{R_s}{k}\frac{V_m}{V_s - V_m} - \frac{R_0}{k}$$

```cpp
}
else
{
    cout << "Game tied";
}
```

- 12.

  ```cpp
  if (x > 0)
  {
      s = 1;
  }
  else if (x < 0)
  {
      s = -1;
  }
  else
  {
      s = 0;
  }
  ```

- 13. You could first set `s` to one of the three values:

  ```cpp
  s = 0;
  if (x > 0) { s = 1; }
  else if (x < 0) { s = -1; }
  ```

- 14. The `if (price <= 100)` can be omitted, making it clear that the `else` branch is the sole alternative.
- 15. No destruction of buildings.
- 16. Add a branch before the final `else`:

  ```cpp
  else if (richter < 0) { cout << "Error: Negative input" << endl; }
  ```

- 17. $3,200.
- 18. No. Then the computation is 0.10 × 32000 + 0.25 (32000 – 32000).
- 19. No. Their individual tax is $5,200 each, and if they married, they would pay $10,400. Actually, taxpayers in higher tax brackets (which our program does not model) may pay higher taxes when they marry, a phenomenon known as the *marriage penalty*.
- 20. Change `else` in line 36 to `else if (marital_status == "m")`, and add another branch after line 47:

  ```cpp
  else { cout << "Error: marital status should be s or m." << endl; }
  ```

- 21. The higher tax rate is only applied on the income in the higher bracket. Suppose you are single and make $31,900. Should you try to get a $200 raise? Absolutely: you get to keep 90 percent of the first $100 and 75 percent of the next $100.
- 22.

  ![](img/5e58fb4c840712efd6ed6fa82bb97f57_154_0.png)

| Test Case | Expected Output | Comment |
|---|---|---|
| (0.5, 0.5) | inside | |
| (4, 2) | outside | |
| (0, 2) | on the boundary | Exactly on the boundary |
| (1.414, 1.414) | on the boundary | Close to the boundary |
| (0, 1.9) | inside | Not less than 1 mm from the boundary |
| (0, 2.1) | outside | Not less than 1 mm from the boundary |

- 31. `x == 0 && y == 0`
- 32. `x == 0 || y == 0`
- 33. `(x == 0 && y != 0) || (y == 0 && x != 0)`
- 34. The same as the value of frozen.
- 35. You are guaranteed that there are no other values. With strings or integers, you would need to check that no values such as "maybe" or −1 enter your calculations.
- 36. (a) Error: The floor must be between 1 and 20. (b) Error: The floor must be between 1 and 20. (c) The elevator will travel to the actual floor 19 (d) Error: Not an integer.
- 37. `cin.fail() || floor == 13 || floor <= 0 || floor > 20`
- 38. Check for `cin.fail()`, to make sure a researcher didn’t supply an input such as oh my. Check for `weight <= 0`, since any rat must surely have a positive weight. We don’t know how giant a rat could be, but the New Guinea rats weighed no more than 2 kg. A regular house rat (*rattus rattus*) weighs up to 0.2 kg, so we’ll say that any weight > 10 kg was surely an input error, perhaps confusing grams and kilograms. Thus, the checks are

  ```cpp
  if (cin.fail())
  {
      cout << "Error: Not a number" << endl;
      return 1;
  }

  if (weight < 0)
  {
      cout << "Error: Weight cannot be negative." << endl;
      return 1;
  }

  if (weight > 10)
  {
      cout << "Error: Weight > 10 kg." << endl;
      return 1;
  }
  ```

- 39. The first input fails. The value of m is unchanged. Because a previous input failed, the next input doesn’t even try to get additional keystrokes. It also fails, and n is unchanged. The program prints 1 2.

## CHAPTER 4: LOOPS

![](img/5e58fb4c840712efd6ed6fa82bb97f57_158_0.png)

### CHAPTER GOALS

- To implement while, for, and do loops
- To avoid infinite loops and off-by-one errors
- To understand nested loops
- To implement programs that read and process data sets
- To use a computer for simulations

### CHAPTER CONTENTS

- 4.1 THE WHILE LOOP 132
- *Syntax 4.1:* while Statement 133
- *Common Error 4.1:* Infinite Loops 136
- *Common Error 4.2:* Don’t Think “Are We There Yet?” 137
- *Common Error 4.3:* Off-by-One Errors 137
- *Random Fact 4.1:* The First Bug 138
- 4.2 PROBLEM SOLVING: HAND-TRACING 139
- 4.3 THE FOR LOOP 142
- *Syntax 4.2:* for Statement 144
- *Programming Tip 4.1:* Use for Loops for Their Intended Purpose Only 147
- *Programming Tip 4.2:* Choose Loop Bounds That Match Your Task 147
- *Programming Tip 4.3:* Count Iterations 147
- 4.4 THE DO LOOP 148
- *Programming Tip 4.4:* Flowcharts for Loops 149
- 4.5 PROCESSING INPUT 150
- *Special Topic 4.1:* Clearing the Failure State 153
- *Special Topic 4.2:* The Loop-and-a-Half Problem and the Break Statement 153
- *Special Topic 4.3:* Redirection of Input and Output 154
- 4.6 PROBLEM SOLVING: STORYBOARDS 154
- 4.7 COMMON LOOP ALGORITHMS 157
- *How To 4.1:* Writing a Loop 162
- *Worked Example 4.1:* Credit Card Processing
- 4.8 NESTED LOOPS 165
- 4.9 RANDOM NUMBERS AND SIMULATIONS 168
- *Random Fact 4.2:* Software Piracy 172
