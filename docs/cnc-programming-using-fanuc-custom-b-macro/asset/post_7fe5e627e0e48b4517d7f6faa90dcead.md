
The problem is more severe in the use of G-codes. The control does not allow any macro expression in the use as a number of a G-code. So, a command such as G[01] is not equivalent to G01, and is illegal. But, one must be aware that the control may not give an error message in all cases. For example, G[03] causes an unexpected tool movement at rapid traverse rate on 0i Mate TC control, which may cause an accident on the machine. So, as a rule of thumb, never use a macro expression as the number of a G-code.

G-codes can, however, use macro variables as their numbers. These variables also can be defined in terms of an arithmetic expression. Though no practical application may ever need to use expressions for defining these variables, one should be aware of even theoretical possibilities, which might be helpful in interpreting the outcome of certain mistakes in the program:

```text
#1 = 0;                         (Stores 0.000 in #1)
#2 = 1;                         (Stores 1.000 in #2)
IF [#2 GT #1] THEN #3 = 99;     (TRUE condition, so #3 becomes 99.000)

#4 = [#2 + #3] / 2;             (Calculation makes #4 equal to 50.000)

G#1;                            (Equivalent to G00)
G#2;                            (Equivalent to G01)
G#3;                            (Equivalent to G99)
G#4;                            (Equivalent to G50)
```

Except a few (e.g., G12.1 and G13.1), all G-code numbers are integers. So, the values of the variables (directly assigned or assigned through an expression), to be used as G-code numbers, must be integers. Fanuc control accepts real numbers also, as long as its rounded form, up to the first place after the decimal point, contains 0 after the decimal point. In other words, it allows an “error” of ±0.05. So, a number in the range 1.95 ≤ n ≤ 2.0499999 is taken as 2.0; in the 2.95 ≤ n ≤ 3.0499999 range, it would be taken as 3.0; whereas 2.05 ≤ n ≤ 2.9499999 is an illegal range (as the range is 2.1 ≤ n ≤ 2.9, in the rounded form). So, 1.95, 2.0, 2.0499999, etc. are all taken as 2, while 1.9499999, 2.05, 2.9499999, etc. would be illegal:

```text
#1 = 1.9499999;
#2 = 1.95;
#3 = 2.0;
#4 = 2.0499999;
#5 = 2.05;

G#1;                            (Illegal)
G#2;                            (Equivalent to G02)
G#3;                            (Equivalent to G02)
G#4;                            (Equivalent to G02)
G#5;                            (Illegal)
```

The purpose of explaining the effect of specifying a real number, in place of an integer, is to fully describe the logic used by typical controls. Logically, a situation where the result of calculation (or direct assignment) comes out to be a real number (with nonzero digits after the decimal point), where an integer is expected (such as the values associated with G-, M- and S-codes), would never arise unless there is some mistake in the program. However, for a quick diagnosis, it is necessary to fully understand the logic built in the macro compiler. Even if the program is perfect, typing mistakes can always creep in.

Recall that parameter 3401#0 decides whether a dimensional value (such as distance and feedrate) expressed as a number without a decimal point would be interpreted as a millimeter value or a micron value (assuming G21 mode). This may cause a serious problem on some controls, other than Fanuc, if an integer number is used in place of a real number, while defining a variable. For example,

```text
#1 = 10;
G00 W#1;
```

may cause a displacement of 0.01 mm. So, to be on the safer side, always use decimal points for all dimensional values. This problem, however, does not exist on Fanuc controls which would store 00010.000 in variable #1, irrespective of parameter setting.

Variables can be used as the values following any letter address except O (program number) and N (sequence number). The optional block skip number also does not allow use of variables:

```text
#1 = 1;
O#1;                 (An illegal statement. Use O1)
N#1 G01 X100;        (An illegal statement. Use N1)
/#1 G01 X100;        (An illegal statement. Use /1)
```

## 2.6 Undefined Variables

If a value is not explicitly assigned to a variable, it remains undefined, and does not contain anything. Such a variable is called a null variable or a vacant variable. #0 is a predefined, read-only-type null variable. No data can be stored in it. It has been provided for the sole purpose of logical comparison of some other variable with it, to find out whether or not the variable is defined. Comparison statements are used in conditional expressions, which are explained in more detail in Secs. 4.1 and 5.2.

### Null Variables in Word Addresses

When a null variable appears in an address, that particular address (only) is ignored. For example, if #1 is a null variable, then G00 X#1 will not cause any movement, though G00 will become the active modal code of Group 1. This statement is equivalent to a sole G00 command, without any axis word. On the other hand, G00 X#1 Z100 is equivalent to G00 Z100.

### Null Variables in Arithmetic Operations

Usually, if a null variable is used somewhere, for a purpose other than a comparison to find out whether or not it is a null variable, an error message, UNDEFINED VARIABLE, would have been more appropriate. But, the Fanuc macro compiler (and possibly compilers of other manufacturers also) is not designed this way. In arithmetic operations such as addition and multiplication, as well as in function evaluation, a null variable is treated as a variable having 0 value. In the following examples, all variables are assumed to be null variables, initially:

| Statement | Explanation |
|---|---|
| `#2 = #1;` | (#2 remains a null variable because there is no arithmetic operation or function evaluation in this statement) |
| `#3 = [#1];` | (Presence of brackets does make it an expression, but absence of any arithmetic operation with #1 keeps it null. So, #3 remains a null variable) |
| `#4 = #1 + #1;` | (Equivalent to #4 = 0 + 0. So, #4 gets defined and stores 0) |
| `#5 = #1 * 5;` | (Equivalent to #5 = 0 * 5. So, #5 gets defined and stores 0) |
| `#6 = 1 / #1;` | (Equivalent to #6 = 1 / 0, which will give “DIVIDED BY ZERO” error) |
| `#7 = SQRT[#1];` | (Equivalent to #7 = SQRT[0]. So, #7 gets defined and stores 0) |
| `#8 = #4109;` | (Variable #4109 contains the currently active feedrate on the machine, and if no F-word has been used anywhere in the preceding program blocks, it contains 0. Hence, #8 would store either the current feedrate or 0. #4109-type variables are described in Chap. 3. These variables are never null, even if not explicitly defined) |

### Null Variables in Conditional Expressions

Except for EQ (equal to) and NE (not equal to), a null variable is the same as 0. In the following statements, #1 is a null variable:

| Statement | Explanation |
|---|---|
| `[#1 LT 0]` | (Equivalent to 0 LT 0, hence FALSE) |
| `[#1 LE 0]` | (Equivalent to 0 LE 0, hence TRUE) |
| `[#1 GT 0]` | (Equivalent to 0 GT 0, hence FALSE) |
| `[#1 GE 0]` | (Equivalent to 0 GE 0, hence TRUE) |
| `[#1 LT #0]` | (Equivalent to 0 LT 0, hence FALSE) |
| `[#1 LE #0]` | (Equivalent to 0 LE 0, hence TRUE) |
| `[#1 GT #0]` | (Equivalent to 0 GT 0, hence FALSE) |
| `[#1 GE #0]` | (Equivalent to 0 GE 0, hence TRUE) |

However, a null variable is not the same as 0 in comparison statements using EQ and NE:

- `[#1 EQ 0]` (With EQ, a null variable is not the same as 0, hence FALSE)
- `[#1 NE 0]` (With NE, a null variable is not the same as 0, hence TRUE)
- `[#1 EQ #0]` (With EQ, a null variable is the same as #0, hence TRUE)
- `[#1 NE #0]` (Both are null variables, hence FALSE)

## 2.7 A Simple Use of Macro Programming Features

Finally, the following simple example shows how the use of variables makes the same program work under different requirements:

```text
#1 = 0;
#10 = 1;
#100 = 50;
#101 = 60;
#102 = 30;
G#10 X#100 Z#101 R#1 F#102;
```

These statements are equivalent to G01 X50.000 Z60.000 R0.000 F30.000, which can be made to do different things simply by changing the values stored in the different variables. There can be several such statements in the program. There is no need to modify any of them. Just define the variables at the beginning of the program, and change them as per requirement. This is the simplest and most effective use of macro programming, which does not require an in-depth knowledge of this programming language. One need only be aware of the types of macro variables and their permissible ranges.

## 2.8 Retaining Programs in MDI Mode

All the statements made above and in the subsequent chapters have actually been verified on Fanuc 0i Mate TC wherever applicable. If one wishes to verify them, or wants to try some other combinations, this can be safely done using the dynamic graphic feature in AUTO mode (automatic operation mode, which is also called memory mode). If, however, no tool movement is involved, verification can be done without using dynamic graphic, in memory mode. In fact, even MDI mode can be used. But the default setting for the MDI mode is such that the program is erased automatically after its execution is complete. This means that the program would have to be typed again, for a subsequent execution. This makes trial and error impractical in MDI mode. However, if parameter 3204#6 is set to 1, the MDI program is retained even after its execution is over. The RESET key will,
