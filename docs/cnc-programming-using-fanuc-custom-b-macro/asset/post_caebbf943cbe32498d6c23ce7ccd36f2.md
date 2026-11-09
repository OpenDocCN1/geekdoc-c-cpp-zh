
```
#[#1] = SQRT[-#21];
G00 W#11;
```

All cases of assigning a value to a variable. (Only eight decimal digits are stored.) (Causes a displacement of 3.162 mm, the rounded value up to three digits after decimal, as the least input increment for displacement is 0.001 mm, in millimeter mode. In an NC statement, rounding of axis values, up to the least input increment of the machine, is automatically done by the control, if the values are specified in terms of variables. Refer to Sec. 4.4 also.)

The term “NC statement” has been used without formally defining it. It is a *program block* involving at least one NC address, such as G, M, F, S, T, X, Y, and Z, except codes for calling a macro program (such as G65, G66, etc.). On the other hand, a *macro statement* simply assigns a value to a variable (#1 = <some value or an arithmetic expression>), or jumps to a specified block number (GOTO_ and IF_GOTO_), or uses a conditional statement (IF_THEN_WHILE_DO_ and END_), or calls a macro program. To put it simply, a macro statement does not directly cause physical machine movement, whereas an NC statement directly controls the machine movement. An NC statement may or may not use macro variables/functions.

There are two major differences in the way the control treats NC statements and macro statements:

- If the program is executed in the single-block mode (there is a switch for this purpose on the MOP), its execution stops at the end of each NC statement, and proceeds to the next block only after the CYCLE START button is pressed again. However, the execution does not stop at the end of a macro statement; it proceeds to the next block. If it is desired to execute the macro statements also in single-block mode, set parameter 6000#5 to 1. In a normal situation, such a requirement would never arise, because a macro statement does not involve machine movement. However, in case of an error in the program, execute the macro statements one at a time to check the intermediate calculations.
- Although the program execution is block by block, the control pre-reads the next block and interprets it in advance, to speed up the execution. In the radius compensation mode, two blocks are preread, because the control needs to position the tool properly at the end of the current block, to suit the next path segment. However, all (or as many as possible) sequential macro statements are read and evaluated immediately. In fact, the control does not count a macro statement as a block. An NC statement constitutes a block.

Coming back to the discussion on defining variables, note that a variable always stores a value with minimum three decimal places, if the total number of digits does not exceed eight. If less than three decimal places are used, zeroes are added.

```
Examples:
#1 = 1234;             (Stores 01234.000)
#1 = 12345;            (Stores 12345.000)
#1 = 123456;           (Stores 123456.000)
#1 = 1234567;          (Stores 1234567.0)
#1 = 12345678;         (Stores 12345678)
```

If more than eight digits are specified, the additional digits might be converted to 0, after rounding up to eight digits (irrespective of decimal position), which may give unexpected results, as explained in the following example:

```
#1 = 123456.789;     (Stores 123456.790 in variable #1)
#2 = 123456.794;     (Stores 123456.790 in variable #2)
#3 = #2 - #1;        (Stores 0.000 in variable #3)
```

However, in the Fanuc 0i control, specifying more than eight digits, for any value, generates an error message, "TOO MANY DIGITS", and terminates the program execution. It will not store values like 123456.789 in a variable, and will display the error message. If, however, more than eight digits result after an arithmetic calculation, rounding is automatically done up to eight digits, and no error (alarm message) or warning (operator’s message) appear.

A variable can also be defined in a conditional manner (conditional statements are explained in Sec. 5.3):

```
#10 = 10;
#25 = 5;
IF [#10 GT #25] THEN #25 = #25 + 10;    (TRUE condition, so
                                           #25 becomes 15.000)
```

### 2.4 Display of Variables

It is necessary to understand how the values of variables are displayed on the macro variable screen, because it might cause some confusion. The calculated value of a variable must lie within the permitted range (10⁻²⁹ ≤ magnitude ≤ 10⁴⁷, or be 0). However, all the legal values cannot be displayed correctly on the screen, which uses a simple eight-digit decimal format, without exponential digits. Even then, the value (provided it is legal) held in the variable is correctly used for further calculations. Also, Fanuc 0i series controls do not allow more than eight digits (including leading or trailing zeroes) for specifying a value in direct assignment. Some examples are given below:

```
#1 = 0.00000001;                 (Illegal value, as it contains
                                  more than eight digits)
#1 = .00000001;
```

(Assigns correct value to #1, but displays nine stars, ********, because the number cannot be correctly displayed using eight digits, because the display automatically adds at least one zero to the left of decimal. So, it should display 0.00000001, which it cannot because nine digits are required. Note that the value is the same as the value in the previous example)

```
#1 = #1 * 10;
```

(Assigns 0.00000001 to #1 which is also correctly displayed)

```
#1 = #1 * #1 * #1 * #1 * #1 / 10;
```

(Assigns 10^-30 to #1, but displays nine stars)

```
#1 = #1 / 10;
```

(The calculated value is less than 10^-38, which does not lie in the permitted range, so the execution terminates with an alarm. Note that the alarm message would be "CALCULATED DATA OVERFLOW," though it is actually a *mathematical underflow*)

```
#1 = 10000000;
```

(Displays 10000000)

```
#1 = #1 * #1 * #1 * #1 * #1 * #1;
```

(Assigns 10^70 to #1, but displays nine stars)

```
#1 = #1 * 100000;
```

(Assigns 10^75 to #1, but displays nine stars)

```
#1 = #1 * 10;
```

(The calculated value is more than 10^77 which does not lie in the permitted range. So, the execution terminates with an alarm, "CALCULATED DATA OVERFLOW")

### 2.5 Real versus Integer Values

Though perhaps inappropriate, Fanuc control is very liberal in the use of real numbers in place of integer numbers, and vice versa, in *macro statements* (only). While integer numbers in place of real numbers do not cause any problem, real numbers (direct assignment or the value of an arithmetic expression) used in place of integer numbers are automatically rounded. This has already been explained with reference to designation numbers of variables. Here are some different examples (once again, this is only a theoretical discussion, with the sole purpose of explaining the logic being followed by the control, as it might help in error diagnosis):

```
#1 = 1000.4999;
M03 S#1;             (Equivalent to M03 S1000)

#1 = 1000.5000;
M03 S#1;          (Equivalent to M03 S1001)
M03 S1000.0;      (An illegal statement. S-value must be an integer number)

#1 = 3.4999999;
M#1 S1000;        (Equivalent to M03 S1000)
#1 = 3.5000000;
M#1 S1000;
M3.0 S1000;       (An illegal statement. M-value must be an integer number)
```

Although the last statement is illegal, if 3.0 (or some other real number or expression) is enclosed within square brackets, it becomes a macro expression, and rounding is done:

```
M[3.0] S1000;       (Equivalent to M03 S1000)
M[3.4999999] S1000; (Equivalent to M03 S1000)
M[3.5] S1000;       (Equivalent to M04 S1000)
```

This also applies to all other addresses (except G-codes) such as spindle speed also:

```
M03 S[1000.0];    (Equivalent to M03 S1000)
M03 S[1000.4999];  (Equivalent to M03 S1000)
M03 S[1000.5000];  (Equivalent to M03 S1001)
```

All these square brackets can also contain arithmetic expressions. Note that if parameter 3451#2 (on a milling machine only; this parameter is not available on a lathe) is set to 1, the spindle speed can have up to one decimal point, though the interpreted speed would be the rounded integer value:

```
S1000.5;   (Equivalent to S1001, if parameter 3451#2 = 1)
S1000.50;  (Illegal, because of more than one decimal place)
```

“Too much flexibility makes a programming language rather ‘undisciplined,’ and it becomes error-prone. An inadvertent mistake by the programmer might be interpreted “correctly” by the machine, leading to undesirable consequences. And this is very possible because macro programming may involve complex calculations and complicated logic. In the author’s opinion, a real value must not be accepted where an integer value is required. Moreover, as has been described in Sec. 2.6, Fanuc control (in fact, perhaps all controls) treats a null variable as a variable having 0 value in arithmetic calculations. This is again illogical and may prove to be dangerous. Typing mistakes are always possible. Perhaps the control manufacturers should modify their macro compilers to make it a PASCAL-like disciplined language. Presently, the programmer has to very meticulously understand the logic followed by the macro compilers.”
