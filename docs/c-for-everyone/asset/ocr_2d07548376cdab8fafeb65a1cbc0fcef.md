**P3.24** Write a program that asks the user to enter a month (1 for January, 2 for February, and so on) and then prints the number of days in the month. For February, print “28 or 29 days”.

```
```text
Enter a month: 5
30 days
```
```

Do not use a separate if/else branch for each month. Use Boolean operators.

**P3.25** A year with 366 days is called a leap year. A leap year is a leap year if it is divisible by four (for example, 1980), except that it is not a leap year if it is divisible by 100 (for example, 1900); however, it is a leap year if it is divisible by 400 (for example, 2000). There were no exceptions before the introduction of the Gregorian calendar on October 15, 1582 (1500 was a leap year). Write a program that asks the user for a year and computes whether that year is a leap year.

**P3.26** Add error handling to Exercise P3.2. If the user does not enter a number when expected, or provides an invalid unit for the altitude, print an error message and end the program.

**Engineering P3.27** Write a program that prompts the user for a wavelength value and prints a description of the corresponding part of the electromagnetic spectrum, as given in Table 7.

![](bbox=[0.11, 0.429, 0.361, 0.525])

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

**Engineering P3.28** Repeat Exercise P3.27, modifying the program so that it prompts for the frequency instead.

**Engineering P3.29** Repeat Exercise P3.27, modifying the program so that it first asks the user whether the input will be a wavelength or a frequency.

**Engineering P3.30** A minivan has two sliding doors. Each door can be opened by either a dashboard switch, its inside handle, or its outside handle. However, the inside handles do not work if a child lock switch is activated. In order for the sliding doors to open, the gear shift must be in *park*, and the master unlock switch must be activated. (This book’s author is the long-suffering owner of just such a vehicle.)

![](bbox=[0.741, 0.794, 0.919, 0.9])