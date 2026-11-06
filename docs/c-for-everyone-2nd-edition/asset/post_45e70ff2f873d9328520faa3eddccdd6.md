
## 2.3.2 Formatted Output

When you print the result of a computation, you often want some control over its appearance. For example, when you print an amount in dollars and cents, you usually want it to be rounded to two digits after the decimal point. That is, you want the output to look like

```
Price per ounce: 0.04
```

instead of

```
Price per ounce: 0.0409722
```

The following command instructs `cout` to use two digits after the decimal point for all floating-point numbers:

```
cout << fixed << setprecision(2);
```

This command does not produce any output; it just manipulates `cout` so that it will change the output format. The values `fixed` and `setprecision` are called *manipulators*. We will discuss manipulators in detail in Chapter 8. For now, just remember to include the statement given above whenever you want currency values displayed neatly.

To use manipulators, you must include the `<iomanip>` header in your program:

```
#include <iomanip>
```

You can combine the manipulators and the values to be displayed into a single statement.

```
cout << fixed << setprecision(2)
     << "Price per ounce: "
     << price_per_ounce << endl;
```

There is another manipulator that is sometimes handy. When you display several rows of data, you usually want the columns to line up.

You use the `setw` manipulator to set the width of the next output field. The width is the total number of characters used for showing the value, including digits, the decimal point, and spaces. Controlling the width is important when you want columns of numbers to line up.

For example, if you want a number to be printed in a column that is eight characters wide, you use

```
cout << setw(8) << price_per_ounce;
```

You use manipulators to specify how values should be formatted.

![](img/23fb3582e93ebc95909e1de029c3d388_76_0.png)

You use manipulators to line up your output in neat columns.

This command prints the value `price_per_ounce` in a field of width 8, for example

```
    0.04
```

(where each ■ represents a space).

There is a notable difference between the `setprecision` and `setw` manipulators. Once you set the precision, that value is used for all floating-point numbers. But the width affects only the *next* value. Subsequent values are formatted without added spaces.

Our next example program will prompt for the price of a six-pack and the volume of each can, then print out the price per ounce. The program puts to work what you just learned about reading input and formatting output.

### ch02/volume2.cpp

```cpp
#include <iostream>
#include <iomanip>

using namespace std;

int main()
{
    // Read price per pack

    cout << "Please enter the price for a six-pack: ";
    double pack_price;
    cin >> pack_price;

    // Read can volume

    cout << "Please enter the volume for each can (in ounces): ";
    double can_volume;
    cin >> can_volume;

    // Compute pack volume

    const double CANS_PER_PACK = 6;
    double pack_volume = can_volume * CANS_PER_PACK;

    // Compute and print price per ounce

    double price_per_ounce = pack_price / pack_volume;

    cout << fixed << setprecision(2);
    cout << "Price per ounce: " << price_per_ounce << endl;

    return 0;
}
```

### Program Run

```
Please enter the price for a six-pack: 2.95
Please enter the volume for each can (in ounces): 12
Price per ounce: 0.04
```

- 20. Translate the pseudocode for computing the number of tiles and the gap width into C++.

- 21. Suppose the architect specifies a pattern with black, gray, and white tiles, like this:

  ![](img/23fb3582e93ebc95909e1de029c3d388_80_0.png)

  Again, the first and last tile should be black. How do you need to modify the algorithm?

- 22. A robot needs to tile a floor with alternating black and white tiles. Develop an algorithm that yields the color (0 for black, 1 for white), given the row and column number. Start with specific values for the row and column, and then generalize.

  ![](img/23fb3582e93ebc95909e1de029c3d388_80_1.png)

  ![](img/23fb3582e93ebc95909e1de029c3d388_80_2.png)

- 23. For a particular car, repair and maintenance costs in year 1 are estimated at $100; in year 10, at $1,500. Assuming that the repair cost increases by the same amount every year, develop pseudocode to compute the repair cost in year 3 and then generalize to year *n*.

- 24. The shape of a bottle is approximated by two cylinders of radius *r₁* and *r₂* and heights *h₁* and *h₂*, joined by a cone section of height *h₃*. Using the formulas for the volume of a cylinder, *V = πr²h*, and a cone section, *V = π(r₁² + r₁r₂ + r₂²)h/3*, develop pseudocode to compute the volume of the bottle. Using an actual bottle with known volume as a sample, make a hand calculation of your pseudocode.

**Practice It** Now you can try these exercises at the end of the chapter: R2.13, R2.15, R2.16.

![](img/23fb3582e93ebc95909e1de029c3d388_80_3.png)

## WORKED EXAMPLE 2.1 — Computing Travel Time

In this Worked Example, we develop a hand calculation to compute the time that a robot requires to retrieve an item from rocky terrain.

![](img/23fb3582e93ebc95909e1de029c3d388_80_4.png)

## HOW TO 2.1 Carrying out Computations

Many programming problems require that you carry out arithmetic computations. This How To shows you how to turn a problem statement into pseudocode and, ultimately, a C++ program.

For example, suppose you are asked to write a program that simulates a vending machine. A customer selects an item for purchase and inserts a bill into the vending machine. The vending machine dispenses the purchased item and gives change. We will assume that all item prices are multiples of 25 cents, and the machine gives all change in dollar coins and quarters. Your task is to compute how many coins of each type to return.

### Step 1

Understand the problem: What are the inputs? What are the desired outputs?

In this problem, there are two inputs:

- The denomination of the bill that the customer inserts
- The price of the purchased item

There are two desired outputs:

- The number of dollar coins that the machine returns
- The number of quarters that the machine returns

### Step 2

Work out examples by hand.

Let’s assume that a customer purchased an item that cost $2.25 and inserted a $5 bill. The customer is due $2.75, or two dollar coins and three quarters.

That is easy for you to see, but how can a C++ program come to the same conclusion? The computation is simpler if you work in pennies, not dollars. The amount due to the customer is 275 pennies. Dividing by 100 yields 2, the number of dollars. Dividing the remainder (75) by 25 yields 3, the number of quarters.

### Step 3

Write pseudocode for computing the answers.

In the previous step, you worked out a specific instance of the problem. You now need to come up with a method that works in general.

Given an arbitrary item price and payment, how can you compute the coins due? First, compute the amount due in pennies:

```
amount due = 100 × bill value - item price in pennies
```

To get the dollars, divide by 100 and discard the remainder:

```
dollar coins = amount due / 100 (without remainder)
```

![](img/23fb3582e93ebc95909e1de029c3d388_81_0.png)

A vending machine takes bills and gives change in coins.

The remaining amount due can be computed in two ways. If you are familiar with the modulus operator, you can simply compute

```
amount due = amount due % 100
```

Alternatively, subtract the penny value of the dollar coins from the amount due:

```
amount due = amount due - 100 × dollar coins
```

To get the quarters due, divide by 25:

```
quarters = amount due / 25
```

### Step 4

Define the variables and constants that you need, and specify their types.

Here, we have five variables:

- bill_value
- item_price
- amount_due
- dollar_coins
- quarters

Should we introduce constants to explain 100 and 25 as `PENNIES_PER_DOLLAR` and `PENNIES_PER_QUARTER`? Doing so will make it easier to convert the program to international markets, so we will take this step.

It is very important that `amount_due` and `PENNIES_PER_DOLLAR` are of type `int` because the computation of `dollar_coins` uses integer division. Similarly, the other variables are integers.

### Step 5

Turn the pseudocode into C++ statements.

If you did a thorough job with the pseudocode, this step should be easy. Of course, you have to know how to express mathematical operations (such as powers or integer division) in C++.

```cpp
amount_due = PENNIES_PER_DOLLAR * bill_value - item_price;
dollar_coins = amount_due / PENNIES_PER_DOLLAR;
amount_due = amount_due % PENNIES_PER_DOLLAR;
quarters = amount_due / PENNIES_PER_QUARTER;
```

### Step 6

Provide input and output.

Before starting the computation, we prompt the user for the bill value and item price:

```cpp
cout << "Enter bill value (1 = $1 bill, 5 = $5 bill, etc.): ";
cin >> bill_value;
cout << "Enter item price in pennies: ";
cin >> item_price;
```

When the computation is finished, we display the result. For extra credit, we use the `setw` manipulator to make sure that the output lines up neatly.

```cpp
cout << "Dollar coins: " << setw(6) << dollar_coins << endl
     << "Quarters:     " << setw(6) << quarters << endl;
```

### Step 7

Include the required headers and provide a `main` function.

We need the `<iostream>` header for all input and output. Because we use the `setw` manipulator, we also require `<iomanip>`. This program does not use any special mathematical functions. Therefore, we do not include the `<cmath>` header.

In the `main` function, you need to define constants and variables (Step 4), carry out computations (Step 5), and provide input and output (Step 6). Clearly, you will want to first get the input, then do the computations, and finally show the output. Define the constants at the beginning of the function, and define each variable just before it is needed.
