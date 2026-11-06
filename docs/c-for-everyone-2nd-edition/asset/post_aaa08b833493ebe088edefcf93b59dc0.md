
- 20.
  ```cpp
  int pairs = (total_width - tile_width) / (2 * tile_width);
  int tiles = 1 + 2 * pairs;
  double gap = (total_width - tiles * tile_width) / 2;
  ```
  Be sure that `pairs` is declared as an int.

- 21. Now there are groups of four tiles (gray/white/gray/black) following the initial black tile. Therefore, the algorithm is now:

  ```text
  number of groups = integer part of (total width - tile width) / (4 x tile width)
  number of tiles = 1 + 4 x number of groups
  ```

  The formula for the gap is not changed.

- 22. Clearly, the answer depends only on whether the row and column numbers are even or odd, so let’s first take the remainder after dividing by 2. Then we can enumerate all expected answers:

  | Row % 2 | Column % 2 | Color |
  |---:|---:|---:|
  | 0 | 0 | 0 |
  | 0 | 1 | 1 |
  | 1 | 0 | 1 |
  | 1 | 1 | 0 |

  In the first three entries of the table, the color is simply the sum of the remainders. In the fourth entry, the sum would be 2, but we want a zero. We can achieve that by taking another modulo operation:

  ```text
  color = ((row % 2) + (column % 2)) % 2
  ```

- 23. In nine years, the repair costs increased by $1,400. Therefore, the increase per year is $1,400 / 9 = $156. The repair cost in year 3 would be $100 + 2 × $156 = $412. The repair cost in year n is $100 + n × $156. To avoid accumulation of roundoff errors, it is actually a good idea to use the original expression that yielded $156, that is

  ```text
  Repair cost in year n = 100 + n x 1400 / 9
  ```

- 24. The pseudocode follows easily from the equations.

  ```text
  bottom volume = π x r₁² x h₁
  top volume = π x r₂² x h₂
  middle volume = π x (r₁² + r₁ x r₂ + r₂²) x h₃ / 3
  total volume = bottom volume + top volume + middle volume
  ```

  Measuring a typical wine bottle yields `r₁ = 3.6, r₂ = 1.2, h₁ = 15, h₂ = 7, h₃ = 6` (all in centimeters). Therefore,

  ```text
  bottom volume = 610.73
  top volume = 31.67
  middle volume = 135.72
  total volume = 778.12
  ```

  The actual volume is 750 ml, which is close enough to our computation to give confidence that it is correct.

- 25. The length is 11. The space counts as a character.
- 26. `str.substr(7, 4)`
- 27. `str = str + "ming";`
- 28. `Hy`
- 29. `cin >> first_name >> middle_initial >> last_name;`

![](img/23fb3582e93ebc95909e1de029c3d388_103_0.png)

One of the essential features of computer programs is their ability to make decisions. Like a train that changes tracks depending on how the switches are set, a program can take different actions, depending on inputs and other circumstances.

In this chapter, you will learn how to program simple and complex decisions. You will apply what you learn to the task of checking user input.

## 3.1 The if Statement

> The if statement allows a program to carry out different actions depending on the nature of the data to be processed.

The if statement is used to implement a decision. When a condition is fulfilled, one set of statements is executed. Otherwise, another set of statements is executed (see Syntax 3.1).

Here is an example using the if statement. In many countries, the number 13 is considered unlucky. Rather than offending superstitious tenants, building owners sometimes skip the thirteenth floor; floor 12 is immediately followed by floor 14. Of course, floor 13 is not usually left empty or, as some conspiracy theorists believe, filled with secret offices and research labs. It is simply called floor 14. The computer that controls the building elevators needs to compensate for this foible and adjust all floor numbers above 13.

Let's simulate this process in C++. We will ask the user to type in the desired floor number and then compute the actual floor. When the input is above 13, then we need to decrement the input to obtain the actual floor. For example, if the user provides an input of 20, the program determines the actual floor as 19. Otherwise, we simply use the supplied floor number.

```cpp
int actual_floor;

if (floor > 13)
{
    actual_floor = floor - 1;
}
else
{
    actual_floor = floor;
}
```

The flowchart in Figure 1 shows the branching behavior.

In our example, each branch of the if statement contains a single statement. You can include as many statements in each branch as you like. Sometimes, it happens that

![](img/23fb3582e93ebc95909e1de029c3d388_103_1.png)

This elevator panel “skips” the thirteenth floor. The floor is not actually missing—the computer that controls the elevator adjusts the floor numbers above 13.

![](img/23fb3582e93ebc95909e1de029c3d388_104_0.png)

![](img/23fb3582e93ebc95909e1de029c3d388_104_1.png)

There is nothing to do in the else branch of the statement. In that case, you can omit it entirely, such as in this example:

```cpp
int actual_floor = floor;

if (floor > 13)
{
    actual_floor--;
} // No else needed
```

See Figure 2 for the flowchart.

The following program puts the if statement to work. This program asks for the desired floor and then prints out the actual floor.

![](img/23fb3582e93ebc95909e1de029c3d388_104_2.png)

> An if statement is like a fork in the road. Depending upon a decision, different parts of the program are executed.

### ch03/elevator1.cpp

```cpp
#include <iostream>

using namespace std;

int main()
{
    int floor;
    cout << "Floor: ";
    cin >> floor;
    int actual_floor;
    if (floor > 13)
    {
        actual_floor = floor - 1;
    }
    else
    {
        actual_floor = floor;
    }

    cout << "The elevator will travel to the actual floor "
         << actual_floor << endl;

    return 0;
}
```

### Program Run

```text
Floor: 20
The elevator will travel to the actual floor 19
```

### Syntax 3.1  if Statement

![](img/23fb3582e93ebc95909e1de029c3d388_105_0.png)

![](img/23fb3582e93ebc95909e1de029c3d388_106_0.png)

1. In some Asian countries, the number 14 is considered unlucky. Some building owners play it safe and skip both the thirteenth and the fourteenth floor. How would you modify the sample program to handle such a building?

2. Consider the following if statement to compute a discounted price:

   ```java
   if (original_price > 100)
   {
       discounted_price = original_price - 20;
   }
   else
   {
       discounted_price = original_price - 10;
   }
   ```

   What is the discounted price if the original price is 95? 100? 105?

3. Compare this if statement with the one in Self Check 2:

   ```java
   if (original_price < 100)
   {
       discounted_price = original_price - 10;
   }
   else
   {
       discounted_price = original_price - 20;
   }
   ```

   Do the two statements always compute the same value? If not, when do the values differ?

4. Consider the following statements to compute a discounted price:

   ```java
   discounted_price = original_price;
   if (original_price > 100)
   {
       discounted_price = original_price - 10;
   }
   ```

   What is the discounted price if the original price is 95? 100? 105?

5. The variables fuel_amount and fuel_capacity hold the actual amount of fuel and the size of the fuel tank of a vehicle. If less than 10 percent is remaining in the tank, a status light should show a red color; otherwise it shows a green color. Simulate this process by printing out either "red" or "green".

**Practice It** Now you can try these exercises at the end of the chapter: R3.3, R3.4, P3.16.

### Programming Tip 3.1

![](img/23fb3582e93ebc95909e1de029c3d388_106_1.png)

#### Brace Layout

Programmers vary in how they align braces in their code. In this book, we follow the simple rule of making { and } line up.

```java
if (floor > 13)
{
    floor--;
}
```

This style makes it easy to spot matching braces.

![](img/23fb3582e93ebc95909e1de029c3d388_106_2.png)

*Properly lining up your code makes your programs easier to read.*
