
When comparing adjacent values, then store the previous value in a variable.

![](img/5e58fb4c840712efd6ed6fa82bb97f57_188_0.png)

One problem remains. When the loop is entered for the first time, previous has not yet been set. You can solve this problem with an initial input operation outside the loop:

```cpp
double input;
double previous;
cin >> previous;
while (cin >> input)
{
    if (input == previous) { cout << "Duplicate input" << endl; }
    previous = input;
}
```

![](img/5e58fb4c840712efd6ed6fa82bb97f57_188_1.png)

## SELF CHECK

- 31. What total is computed when no user input is provided in the algorithm in Section 4.7.1?
- 32. How do you compute the total of all positive inputs?
- 33. What is the value of position when no match is found in the algorithm in Section 4.7.3?
- 34. What is wrong with the following loop for finding the position of the first space in a string?

```cpp
bool found = false;
for (int position = 0; !found && position < str.length(); position++)
{
    string ch = str.substr(position, 1);
    if (ch == " ") { found = true; }
}
```

- 35. How do you find the last space in a string?
- 36. What is wrong with the following loop for finding the smallest input value?

```cpp
double smallest = 0;
double input;
while (cin >> input)
{
    if (input < smallest)
    {
        smallest = input;
    }
}
```

- 37. What happens with the algorithm in Section 4.7.5 when no input is provided at all?

**Practice It**  Now you can try these exercises at the end of the chapter: P4.8, P4.13, P4.14.

## 4.8 Nested Loops

When the body of a loop contains another loop, the loops are nested. A typical use of nested loops is printing a table with rows and columns.

In Section 3.4, you saw how to nest two if statements. Similarly, complex iterations sometimes require a nested loop: a loop inside another loop statement. When processing tables, nested loops occur naturally. An outer loop iterates over all rows of the table. An inner loop deals with the columns in the current row.

In this section you will see how to print a table. For simplicity, we will simply print powers xⁿ, as in the table at right. Here is the pseudocode for printing the table:

```text
Print table header.
For x from 1 to 10
    Print table row.
    Print endl.
```

|  | x¹ | x² | x³ | x⁴ |
|---|---:|---:|---:|---:|
| 1 | 1 | 1 | 1 | 1 |
| 2 | 2 | 4 | 8 | 16 |
| 3 | 3 | 9 | 27 | 81 |
| … | … | … | … | … |
| 10 | 10 | 100 | 1000 | 10000 |

How do you print a table row? You need to print a value for each exponent. This requires a second loop:

```text
For n from 1 to 4
    Print xⁿ.
```

This loop must be placed inside the preceding loop. We say that the inner loop is nested inside the outer loop (see Figure 7).

![](img/5e58fb4c840712efd6ed6fa82bb97f57_192_0.png)

**Figure 7**  
Flowchart of a Nested Loop

![](img/5e58fb4c840712efd6ed6fa82bb97f57_195_0.png)

- 38. Why is there a statement `cout << endl` in the outer loop but not in the inner loop?
- 39. How would you change the program so that all powers from $x^0$ to $x^5$ are displayed?
- 40. If you make the change in Self Check 39, how many values are displayed?
- 41. What do the following nested loops display?
- 42. Write nested loops that make the following pattern of brackets:

```cpp
for (int i = 0; i < 3; i++)
{
    for (int j = 0; j < 4; j++)
    {
        cout << i + j;
    }
    cout << endl;
}
```

```text
[][][][]
[][][][]
[][][][]
```

**Practice It**  Now you can try these exercises at the end of the chapter: R4.23, P4.21, P4.22.

## 4.9 Random Numbers and Simulations

In a simulation, you use the computer to simulate an activity in the real world. You can simulate an activity. You can introduce randomness by calling the random number generator.

A *simulation program* uses the computer to simulate an activity in the real world (or an imaginary one). Simulations are commonly used for predicting climate change, analyzing traffic, picking stocks, and many other applications in science and business. In the following sections, you will learn how to implement simulations that model phenomena with a degree of randomness.

### 4.9.1 Generating Random Numbers

Many events in the real world are difficult to predict with absolute precision, yet we can sometimes know the average behavior quite well. For example, a store may know from experience that a customer arrives every five minutes. Of course, that is an average—customers don’t arrive in five minute intervals. To accurately model customer traffic, you want to take that random fluctuation into account. Now, how can you run such a simulation in the computer?

The C++ library has a *random number generator*, which produces numbers that appear to be completely random. Calling `rand()` yields a random integer between 0 and `RAND_MAX` (which is an implementation-dependent constant, typically, but not always, the largest valid int value). Call `rand()` again, and you get a different number. The `rand` function is declared in the `<cstdlib>` header.

The following program calls the rand function ten times.

**ch04/random.cpp**

```cpp
#include <iostream>
#include <cstdlib>

using namespace std;

int main()
{
    for (int i = 1; i <= 10; i++)
    {
        int r = rand();
        cout << r << endl;
    }
    return 0;
}
```

## Program Run

```text
1804289383
846930886
1681692777
1714636915
1957747793
424238335
719885386
1649760492
596516649
118964142
```

Actually, the numbers are not completely random. They are drawn from sequences of numbers that don’t repeat for a long time. These sequences are actually computed from fairly simple formulas; they just behave like random numbers. For that reason, they are often called **pseudorandom numbers**.

Try running the program again. You will get the *exact same output*! This confirms that the random numbers are generated by formulas. However, when running simulations, you don’t always want to get the same results. To overcome this problem, specify a **seed** for the random number sequence. Every time you use a new seed, the random number generator starts generating a new sequence. The seed is set with the `srand` function. A simple value to use as a seed is the current time:

```cpp
srand(time(0));
```

Simply make this call once in your program, before generating any random numbers. Then the random numbers will be different in every program run. Also include the `<ctime>` header that declares the time function.

### 4.9.2 Simulating Die Tosses

In actual applications, you need to transform the output from the random number generator into different ranges. For example, to simulate the throw of a die, you need random numbers between 1 and 6.

![](img/5e58fb4c840712efd6ed6fa82bb97f57_196_0.png)

Here is the general recipe for computing random integers between two bounds `a` and `b`. As you know from Programming Tip 4.3 on page 147, there are `b - a + 1` values between `a` and `b`, including the bounds themselves. First compute `rand() % (b - a + 1)` to obtain a random value between 0 and `b - a`, then add `a`, yielding a random value between `a` and `b`:

```cpp
int r = rand() % (b - a + 1) + a;
```

Here is a program that simulates the throw of a pair of dice.

## **ch04/dice.cpp**

```cpp
#include <iostream>
#include <string>
#include <cstdlib>
#include <ctime>

using namespace std;

int main()
{
    srand(time(0));

    for (int i = 1; i <= 10; i++)
    {
        int d1 = rand() % 6 + 1;
        int d2 = rand() % 6 + 1;
        cout << d1 << " " << d2 << endl;
    }
    cout << endl;
    return 0;
}
```

## Program Run

```text
5 1
2 1
1 2
5 1
1 2
6 4
4 4
6 1
6 3
5 2
```

### 4.9.3 The Monte Carlo Method

The Monte Carlo method is an ingenious method for finding approximate solutions to problems that cannot be precisely solved. (The method is named after the famous casino in Monte Carlo.) Here is a typical example: It is difficult to compute the number π, but you can approximate it quite well with the following simulation.

Simulate shooting a dart into a square surrounding a circle of radius 1. That is easy: generate random x and y coordinates between −1 and 1.

![](img/5e58fb4c840712efd6ed6fa82bb97f57_197_0.png)
