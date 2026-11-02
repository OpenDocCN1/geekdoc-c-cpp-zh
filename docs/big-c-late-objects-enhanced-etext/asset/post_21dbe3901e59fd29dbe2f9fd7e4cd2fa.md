
decimal point, and spaces. Controlling the width is important when you want columns of numbers to line up.

For example, if you want a number to be printed in a column that is eight characters wide, you use

```cpp
cout << setw(8) << price_per_ounce;
```

This command prints the value price_per_ounce in a field of width 8, for example

![](img/d61019b035dd82beb581604273c0ee6b_85_0.png)

(where each □ represents a space).

There is a notable difference between the setprecision and setw manipulators. Once you set the precision, that value is used for all floating-point numbers in that statement. But the width affects only the next value. Subsequent values are formatted without added spaces.

Our next example program will prompt for the price of a six-pack and the volume of each can, then print out the price per ounce. The program puts to work what you just learned about reading input and formatting output.

### sec03/volume2.cpp

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

```text
Please enter the price for a six-pack: 2.95
Please enter the volume for each can (in ounces): 12
Price per ounce: 0.04
```

### Table 8 Formatting Output

| Output Statement | Output | Comment |
|---|---|---|
| cout << 12.345678; | 12.3457 | By default, a number is printed with 6 significant digits. |
| cout << fixed << setprecision(2) << 12.3; | 12.30 | Use the fixed and setprecision manipulators to control the number of digits after the decimal point. |
| cout << ":" << setw(6) << 12; | : 12 | Four spaces are printed before the number, for a total width of 6 characters. |
| cout << ":" << setw(2) << 123; | :123 | If the width is not sufficient, it is ignored. |
| cout << setw(6) << ":" << 12; | :12 | The width only refers to the next item. Here, the : is preceded by five spaces. |

### 2.4 Problem Solving: First Do It By Hand

A very important step for developing an algorithm is to first carry out the computations by hand. If you can't compute a solution yourself, it's unlikely that you'll be able to write a program that automates the computation.

To illustrate the use of hand calculations, consider the following problem.

A row of black and white tiles needs to be placed along a wall. For aesthetic reasons, the architect has specified that the first and last tile shall be black. Your task is to compute the number of tiles needed and the gap at each end, given the space available and the width of each tile.

![](img/d61019b035dd82beb581604273c0ee6b_86_0.png)

Pick concrete values for a typical situation to use in a hand calculation.

To make the problem more concrete, let's assume the following dimensions:

- Total width: 100 inches
- Tile width: 5 inches

The obvious solution would be to fill the space with 20 tiles, but that would not work—the last tile would be white.

Instead, look at the problem this way: The first tile must always be black, and then we add some number of white/black pairs:

![](img/d61019b035dd82beb581604273c0ee6b_87_0.png)

The first tile takes up 5 inches, leaving 95 inches to be covered by pairs. Each pair is 10 inches wide. Therefore the number of pairs is 95 / 10 = 9.5. However, we need to discard the fractional part because we can't have fractions of tile pairs.

Therefore, we will use 9 tile pairs or 18 tiles, together with the initial black tile. Altogether, we require 19 tiles.

The tiles span 19 × 5 = 95 inches, leaving a total gap of 100 – 19 × 5 = 5 inches. The gap should be evenly distributed at both ends. At each end, the gap is (100 – 19 × 5) / 2 = 2.5 inches.

This computation gives us enough information to devise an algorithm with arbitrary values for the total width and tile width.

number of pairs = integer part of (total width - tile width) / (2 x tile width)
number of tiles = 1 + 2 x number of pairs
gap at each end = (total width - number of tiles x tile width) / 2

As you can see, doing a hand calculation gives enough insight into the problem that it becomes easy to develop an algorithm.

### EXAMPLE CODE

See sec04 of your companion code for a program that implements this algorithm.

![](img/d61019b035dd82beb581604273c0ee6b_87_1.png)

### WORKED EXAMPLE 2.1: Computing Travel Time

Learn how to develop a hand calculation to compute the time that a robot requires to retrieve an item from rocky terrain. See your E-Text or visit wiley.com/go/bc103.

![](img/d61019b035dd82beb581604273c0ee6b_87_2.png)

Courtesy of NASA.

![](img/d61019b035dd82beb581604273c0ee6b_87_3.png)

### HOW TO 2.1: Carrying out Computations

Many programming problems require that you carry out arithmetic computations. This How To shows you how to turn a problem statement into pseudocode and, ultimately, a C++ program.

### Problem Statement

Suppose you are asked to write a program that simulates a vending machine. A customer selects an item for purchase and inserts a bill into the vending machine. The vending machine dispenses the purchased item and gives change. We will assume that all item prices are multiples of 25 cents, and the machine gives all change in dollar coins and quarters. Your task is to compute how many coins of each type to return.

### Step 1

Understand the problem: What are the inputs? What are the desired outputs?

In this problem, there are two inputs:

- The denomination of the bill that the customer inserts
- The price of the purchased item

There are two desired outputs:

- The number of dollar coins that the machine returns
- The number of quarters that the machine returns

### Step 2 Work out examples by hand.

Let's assume that a customer purchased an item that cost $2.25 and inserted a $5 bill. The customer is due $2.75, or two dollar coins and three quarters.

That is easy for you to see, but how can a C++ program come to the same conclusion? The computation is simpler if you work in pennies, not dollars. The change due to the customer is 275 pennies. Dividing by 100 yields 2, the number of dollars. Dividing the remainder (75) by 25 yields 3, the number of quarters.

### Step 3 Write pseudocode for computing the answers.

In the previous step, you worked out a specific instance of the problem. You now need to come up with a method that works in general.

Given an arbitrary item price and payment, how can you compute the change due in coins?

First, compute the change due in pennies:

*change due = 100 x bill value - item price in pennies*

To get the dollars, divide by 100 and discard the remainder:

*dollar coins = change due / 100 (without remainder)*

The remaining amount due can be computed in two ways. If you are familiar with the modulus operator, you can simply compute

*change due = change due % 100*

Alternatively, subtract the penny value of the dollar coins from the change due:

*change due = change due - 100 x dollar coins*

To get the quarters due, divide by 25:

*quarters = change due / 25*

### Step 4 Define the variables and constants that you need, and specify their types.

Here, we have five variables:

- bill_value
- item_price
- change_due
- dollar_coins
- quarters

![](img/d61019b035dd82beb581604273c0ee6b_88_0.png)

```cpp
20 change_due = change_due % PENNIES_PER_DOLLAR;
21 int quarters = change_due / PENNIES_PER_QUARTER;
22
23 cout << "Dollar coins: " << setw(6) << dollar_coins << endl
24 << "Quarters: " << setw(6) << quarters << endl;
25
26 return 0;
27 }
```

### Program Run

```text
Enter bill value (1 = $1 bill, 5 = $5 bill, etc.): 5
Enter item price in pennies: 225
Dollar coins: 2
Quarters: 3
```

### WORKED EXAMPLE 2.2: Computing the Cost of Stamps

Learn how to use arithmetic functions to simulate a stamp vending machine. See your E-Text or visit wiley.com/go/bc103.

### 2.5 Strings

Strings are sequences of characters.

Many programs process text, not numbers. Text consists of characters: letters, numbers, punctuation, spaces, and so on. A string is a sequence of characters. For example, the string "Harry" is a sequence of five characters.

![](img/d61019b035dd82beb581604273c0ee6b_90_1.png)

© cssxboy/iStockphoto.

### 2.5.1 The string Type

You can define variables that hold strings.

```cpp
string name = "Harry";
```

The string type is a part of the C++ standard. To use it, simply include the header file, `<string>`:

```cpp
#include <string>
```
