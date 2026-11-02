# Program Run

```
```
Please enter the price for a six-pack: 2.95
Please enter the volume for each can (in ounces): 12
Price per ounce: 0.04
```
```

# Table 8 Formatting Output

| Output Statement | Output | Comment |
|---|---|---|
| cout << 12.345678; | 12.3457 | By default, a number is printed with 6 significant digits. |
| cout << fixed << setprecision(2) << 12.3; | 12.30 | Use the fixed and setprecision manipulators to control the number of digits after the decimal point. |
| cout << ":" << setw(6) << 12; | : 12 | Four spaces are printed before the number, for a total width of 6 characters. |
| cout << ":" << setw(2) << 123; | :123 | If the width not sufficient, it is ignored. |
| cout << setw(6) << ":" << 12; | :12 | The width only refers to the next item. Here, the : is preceded by five spaces. |

# 2.4 Problem Solving: First Do It By Hand

A very important step for developing an algorithm is to first carry out the computations by hand. If you can't compute a solution yourself, it's unlikely that you'll be able to write a program that automates the computation.

To illustrate the use of hand calculations, consider the following problem.

A row of black and white tiles needs to be placed along a wall. For aesthetic reasons, the architect has specified that the first and last tile shall be black. Your task is to compute the number of tiles needed and the gap at each end, given the space available and the width of each tile.

![](bbox=[0.4, 0.85, 0.85, 0.95])

Pick concrete values for a typical situation to use in a hand calculation.

To make the problem more concrete, let's assume the following dimensions:

+   - Total width: 100 inches
+   - Tile width: 5 inches

The obvious solution would be to fill the space with 20 tiles, but that would not work—the last tile would be white.