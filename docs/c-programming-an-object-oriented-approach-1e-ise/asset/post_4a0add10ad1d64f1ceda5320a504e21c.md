
Let us analyze the outputs: The first output defines $0! = 1$, which is according to the definition. The second output is obvious; when $n$ is 4, we have $4! = 1 \times 2 \times 3 \times 4 = 24$. The third output shows that the factorial calculation really becomes large when $n$ is 12. The results of the fourth and fifth outputs are strange. The result of $30!$ is less than the result of $22!$. This means overflow has occurred, but we do not know where. It could have occurred for values less than $n = 22$.

## 5.7.3 Power

Another interesting example of multiplication is calculating the power of a number ($b^n$) in which $b$ is called the base and $n$ is called the exponent.

### Understand the Problem

This is an example of multiplication in which the list is the repetition of the same value, the base. In other words, we multiply the base $n$ times by itself.

$\mathit{power} = b^n = b \times b \times b \times \ldots \times b \times b$   *n times*

The library of C++ provides a function that calculates the power of any base to any exponent. The numbers used in this function are all floating-point values. Sometimes we need to use unsigned integers, which is what we do in this section.

### Develop the Algorithm

The following is the informal description of the algorithm.

1. **Input**
   a. *input base*
   b. *input exponent*
2. **Initialize**
   a. *power to 1*
   b. *set counter to 0*
3. **Repeat as long as the counter is less than *exponent***
   a. *set new power to previous power times base*
   b. *update counter*
4. **Output**
   a. *output power*

### Write the Program

Since we know how to handle overflow, we give the final version of the program in Program 5.20.

**Program 5.20** Calculating a base to a power ($b^n$)

```cpp
/************************************************************
 * It uses the idea of multiplication to find the value of a   *
 * base to the power of an exponent (b^n).                     *
 ************************************************************ */
#include <iostream>
using namespace std;

int main ( )
{
    // Variable declaration
    int base, exponent;
    unsigned long int power, temp;
    bool overflow;
    // input validation for base
    do
    {
        cout << "Enter a non-negative integer value for b: ";
        cin >> base;
    } while (base < 0);
    // input validation for exponent
    do
    {
        cout << "Enter a non-negative integer value for n: ";
        cin >> exponent;
    } while (exponent < 0);
    // initialization
    power = 1;
    temp = power;
    overflow = false;
    // Processing
    for (int i = 1; (i <= exponent) && (!overflow); i++)
    {
        power *= base;
        if (power / base != temp)
        {
            overflow = true; // terminate the loop
        }
        temp = power;
    }
    // Output
    if (overflow)
    {
        cout << "Overflow occurred! Try again with smaller b or n.";
    }
    else
    {
        cout << base << "^" << exponent << " = " << power;
    }
    return 0;
}
```

```text
Run:
Enter a non-negative integer value for b: 22
Enter a non-negative integer value for n: 5
22^5 = 5153632

Run:
Enter a non-negative integer value for b: 5
Enter a non-negative integer value for n: 25
5^25 = 298023223876953125

Run:
Enter a non-negative integer value for b: 5
Enter a non-negative integer value for n: 28
Overflow occurred! Try again with smaller b or n.
```

The first point about Program 5.20 is that we may be tempted to allow negative values for $b$ (the base). If we do so, the result would be negative when the value of $n$ (the exponent) is odd. Therefore, we use an unsigned value for power and temp to keep the overflow checking simple.

The second point is that the variable power overflows in the last test, which means our system cannot accept 5^28. The difference between this problem and the previous one is that the overflow depends on the value of $b$ and $n$ together. So it is more difficult to determine what caused overflow.

## 5.7.4 The Smallest and the Largest

Two other common activities in computer science are to find the smallest and the largest values among a list of numbers.

### Understand the Problem

Assume that we have the following list of numbers: 17, 14, 12, 18, and 71. We initialize the variable smallest to +infinity before entering the loop. In each step, we determine the smaller between the result of the last iteration and the next number. We do this by using an if statement. The following demonstrates the process for the smallest. The process for the largest is similar. We set the variable largest to −infinity before entering the loop. In each iteration, we determine the larger between the previous largest and the next number.

| Numbers | smallest = +∞ |
|---|---|
| 17 | smallest = smaller of 17 and previous smallest (+∞) = 17 |
| 14 | smallest = smaller of 14 and previous smallest (17) = 14 |
| 12 | smallest = smaller of 12 and previous smallest (14) = 12 |
| 18 | smallest = smaller of 18 and previous smallest (12) = 12 |
| 71 | smallest = smaller of 71 and previous smallest (12) = 12 |
| **Result** | **12** |

Some literature initializes smallest (or largest) to the first number. Although this practice works for almost all cases, it does not work if the list is empty. In other words, it is not a general solution. You may wonder why we set *smallest* to +infinity. The reason is that we want *smallest* to be the value of the first number in the list after the first iteration. The procedure is similar for *largest*.

### Develop the Algorithm

The following is the informal description of the algorithm.

1. **Input**
   a. input *size*
2. **Initialize**
   a. initialize smallest to (+∞)
   b. initialize largest to (−∞)
   c. initialize counter to 0
3. **Repeat** as long as the counter is less than *size*
   a. read next number
   b. set smallest to the smaller of previous smallest and the number
   c. set largest to the larger of previous largest and the number
   d. update counter
4. **Output**
   a. output smallest
   b. output largest

### Write the Program

Program 5.21 shows how we can combine the components we discussed to find the smallest and the largest among a list of integers.

**Program 5.21** Finding the smallest and the largest in a list

```cpp
/********************************************************
 * The program finds the smallest and the largest among a list
 * of integers when the size of the list is known.
 ********************************************************/
#include <iostream>
#include <limits>          // Header file for numeric limits
using namespace std;

int main ( )
{
    // Variable declaration
    int size;
    int number, smallest, largest;
    // Initialization
    smallest = numeric_limits <int> :: max();
    largest = numeric_limits <int> :: min( );
    // Size Input
    do
    {
        cout << "Enter the size of the list (non-negative): ";
        cin >> size;
    } while (size <= 0);
    // Processing
    for (int i = 1; i <= size; i++)
    {
        cout << "Enter the next item: ";
        cin >> number;
        if (number < smallest)
        {
            smallest = number;
        }
        if (number > largest)
        {
            largest = number;
        }
    } // End for
    // Result output
    cout << "The smallest item is: " << smallest << endl;
    cout << "The largest item is: " << largest << endl;
    return 0;
}
```

```text
Run:
Enter the size of the list (non-negative): 6
Enter the next item: 12
Enter the next item: -3
Enter the next item: 14
Enter the next item: 15
Enter the next item: 27
Enter the next item: -7
The smallest item is: -7
The largest item is: 27

Run:
Enter the size of the list (non-negative): 3
Enter the next item: 1
Enter the next item: 87
Enter the next item: 45
The smallest item is: 1
The largest item is: 87
```
