
![](img/1341ce50369ce8fcfb8dc3539d51c52f_101_0.png)

| Execution trace | Counter | #500 | #501 | #502 | ... | #999 |
|---|---:|---|---|---|---|---|
| Initial values of counter and variables | 500 | old | old | old | old | old |
| Values after executing I loop | 501 | null | old | old | old | old |
| Values after executing II loop | 502 | null | null | old | old | old |
| Values after executing III loop | 503 | null | null | null | old | old |
| Values after executing 499th loop | 999 | null | null | null | null | old |
| Values after executing 500th loop | 1000 | null | null | null | null | null |

**FIGURE 5.2** Flowchart and execution trace of an algorithm for clearing all permanent common variables.

```
N10 #1 = #1 + 1;                         (COUNTER incremented by 1, for selecting the next variable)
IF [#1 LE 999] GOTO 10;                  (Branches to 10 if #1 is less than or equal to 999, i.e., if all variables up to #999 are not cleared)

M30;
```

A more complex example is to calculate the sample standard deviation ($\sigma_{n-1}$) of, say, 10 given numbers which are stored in #1 through #10. The mathematical formula is

$$\bar{x}=\frac{\sum x_i}{n}$$

$$\sigma_{n-1}=\sqrt{\frac{\sum(x_i-\bar{x})^2}{n-1}}$$

where
- $x_i$ = individual data
- $n$ = the total number of data
- $\bar{x}$ = the average value of the given data

The flowchart of an algorithm for calculating $\sigma_{n-1}$ is given in Fig. 5.3. Program number 8002 is based on this algorithm. Although any values can be stored in the variables #1 to #10, the chosen values in this example are 1, 2, 3, ..., 10, respectively. The obtained answer would be 3.0276503. This program can be used for calculating $\sigma_{n-1}$ for up to 33 numbers, stored in #1 through #33.

![](img/1341ce50369ce8fcfb8dc3539d51c52f_102_0.png)

**FIGURE 5.3** Flowchart of an algorithm for calculating the sample standard deviation.

```
O8002 (STANDARD DEVIATION CALCULATION);
(#1 THROUGH #10 @ DATA);
(STORE DESIRED VALUES IN #1...#10);
(#100 = NUMBER OF GIVEN DATA);
(SET #100 TO THE NUMBER OF DATA);
(#101 @ COUNTER);
(#102 @ SUM OF GIVEN DATA);
(#103 @ AVERAGE OF GIVEN DATA);
(#104 @ SUM OF SQUARE DEVIATION);
(#105 @ MEAN SQUARE DEVIATION);
(#501 @ STANDARD DEVIATION);
;

#1 = 1;                        (First data)
#2 = 2;                        (Second data)
#3 = 3;                        (Third data)
#4 = 4;                        (Fourth data)
#5 = 5;                        (Fifth data)
#6 = 6;                        (Sixth data)
#7 = 7;                        (Seventh data)
#8 = 8;                        (Eighth data)
#9 = 9;                        (Ninth data)
#10 = 10;                      (Tenth data. Note that the data-entry
                                step is not shown in the flowchart)
#100 = 10;                     (NUMBER of data)
#101 = 1;                      (Initial value of COUNTER)
#102 = #1;                     (Initial SUM set to the first data)
N10 #101 = #101 + 1;           (COUNTER incremented by 1)
#102 = #102 + #[#101];         (Next data added to SUM)
IF [#101 LT #100] GOTO 10;     (Branching to N10 if all data are not
                                added to SUM)
#103 = #102 / #100;            (AVERAGE calculated)
#101 = 1;                      (COUNTER initialized to 1)
#104 = [#103 - #1] * [#103 - #1];
                                (Initial SUM OF SQUARE DEVIA-
                                TION set to the square deviation for
                                the first data)
N20 #101 = #101 + 1;           (COUNTER incremented by 1)
#104 = #104 + [#103 - #[#101]] * [#103 - #[#101]];
                                (Square deviation for the next
                                data added to SUM OF SQUARE
                                DEVIATION)
IF [#101 LT #100] GOTO 20;     (Branching to N20 if square devia-
                                tions for all data are not added to
                                SUM OF SQUARE DEVIATION)
#105 = #104 / [#100 - 1];      (MEAN SQUARE DEVIATION
                                calculated)
#501 = SQRT[#105];             (STANDARD DEVIATION calcu-
                                lated and stored in the permanent
                                common variable #501)
M30;
```

Note that, on a 7.2-in LCD screen, it is not possible to continuously type more than 34 characters in one block, using the MDI keys. In a complex mathematical calculation, more than 34 characters in a block do appear. For example, in the standard deviation program, there is a block (the one next to the N20 block) with 40 characters. The only way to have such blocks in a program is to first type the program on a PC, and then download it to the CNC through the RS-232C port. This way, a block with practically any number of characters can be used in a program. If, however, the program is typed by using MDI keys only, a long block (with more than 34 characters) would need to be split into smaller blocks. For example,

```
#104 = #104 + [#103 - #[#101]] * [#103 - #[#101]];
```

can be split into smaller blocks in the following manner, which will have the same effect:

```
#111 = #103 - #[#101];

#111 = #111 * #111;
#104 = #104 + #111;
```

(A new variable #111 introduced for intermediate calculations)

The next example finds the roots of a quadratic equation in the form

$$ax^2 + bx + c = 0$$

The formula for the two roots is

$$x_1 = \frac{-b + \sqrt{b^2 - 4ac}}{2a} \qquad\text{and}\qquad x_2 = \frac{-b - \sqrt{b^2 - 4ac}}{2a}$$

The flowchart of an algorithm for finding the two roots is shown in Fig. 5.4. In program number 8003, which is based on this algorithm, any values can be assigned to the variables corresponding to a, b, and c. Here, 1, 1, and −2 have been taken, which give 1 and −2 as the solution for the two roots.

![](img/1341ce50369ce8fcfb8dc3539d51c52f_105_0.png)

**FIGURE 5.4** Flowchart of an algorithm for finding roots of a quadratic equation.

```
O8003 (QUADRATIC EQUATION SOLUTION);
(FORM @ A * X * X + B * X + C = 0);
(#1 @ A);
(#2 @ B);
(#3 @ C);
(ASSIGN DESIRED VALUES TO A,B,C);
(#100 @ DISCRIMINANT);
(#502 @ ROOT1);
(#503 @ ROOT2);
;
#1 = 1;                         (a, i.e. coefficient of x²)
#2 = 1;                         (b, i.e., coefficient of x)
#3 = -2;                        (c, i.e., constant term)
#100 = #2 * #2 - 4 * #1 * #3;   (Determinant calculated)

IF [ABS[#100] LT 0.000001] GOTO 10;          (Branching to N10 if determinant
                                               is 0)

IF [#100 LT 0] THEN #3000 = 1 (IMAG ROOTS);  ("3001 IMAG ROOTS" displayed
                                               and execution terminated, for a
                                               negative determinant. IF_THEN
                                               statement is described in detail in
                                               Sec. 5.3)

#502 = [-#2 + SQRT[#100]] / [2 * #1];         (First root calculated and stored
                                               in the permanent common variable #502)
#503 = [-#2 - SQRT[#100]] / [2 * #1];         (Second root calculated and stored
                                               in another permanent common variable #503)
GOTO 20;                                      (Branching to N20)
N10 #502 = -#2 / [2 * #1];                    (First root calculated, when the determinant is 0)
#503 = #502;                                  (The two roots are equal)
N20 M30;
```

Recall that every macro calculation typically involves an error of $10^{-6}$. So, even if the determinant is actually 0, it may not come out to be *exactly 0*. It is because of this reason that the absolute value of the determinant is being checked against a small value, in this program.

Note that, even if the determinant is negative, generating an alarm, the permanent common variables #502 and #503 would still have old values (if any) stored in them. If this is likely to cause a confusion, set #502 and #503 to null (#0), if the determinant comes out to be negative. In fact, as already stated, a good programming practice would be to *unconditionally* set these variables to null in the very beginning of the program. This applies to all programs which use permanent common variables, without needing their old values.

For additional practice, the reader may try to develop programs for finding

- The largest and the smallest number in a given set of data
- The sum of a finite series of the type $\sum_i^n$ (an expression in terms of index i)
- The sum of an infinite but convergent series (the calculation would need to be terminated when a series term is found to be very small, say, less than 0.000001)
- The calculation of factorial of a given number, etc.

Wherever possible, *recurrence relation* should be used for computational efficiency. For example, the factorial of a given number can be defined in terms of the factorial of its preceding number: $i! = (i - 1)! \times i$. Such a technique is especially advantageous in series summation. An example is given below:

$$\mathrm{sum} = x - \frac{x^3}{3!} + \frac{x^5}{5!} - \frac{x^7}{7!} + \cdots + (-1)^{n-1}\frac{x^{2n-1}}{(2n-1)!}$$

An inspection indicates that

$i$th term = $(-1)^{i-1}\frac{x^{2i-1}}{(2i-1)!}$ and $(i+1)$th term = $(-1)^i\frac{x^{2i+1}}{(2i+1)!}$
