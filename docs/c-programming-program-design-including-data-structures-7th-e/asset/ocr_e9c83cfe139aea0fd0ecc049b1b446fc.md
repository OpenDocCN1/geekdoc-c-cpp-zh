# EXAMPLE 6-5 (FIBONACCI NUMBER)

In the first programming example in Chapter 5, we designed and implemented an algorithm to find the number of a Fibonacci sequence. In this example, we modify the main program by writing a function that computes and returns the desired number of a Fibonacci sequence. Because we have already designed and discussed how to determine a specific number of a Fibonacci sequence, next, we give the definition of the function to implement the algorithm.

Given the first number, the second number, and the position of the desired Fibonacci number, the following function returns the Fibonacci number:

```
```cpp
int nthFibonacciNum(int first, int second, int nthFibNum)
{
    int current;
    int counter;

    if (nthFibNum == 1)
        current = first;
    else if (nthFibNum == 2)
        current = second;
    else
    {
        counter = 3;

        while (counter <= nthFibNum)
        {
            current = second + first;
            first = second;
            second = current;
            counter++;
        } //end while
    } //end else

    return current;
}
```
```

The following shows how to use this function in a program.

```
```cpp
//Program: Fibonacci number
#include <iostream>
using namespace std;

int nthFibonacciNum(int first, int second, int position);

int main()
{
    int firstFibonacciNum;
    int secondFibonacciNum;
    int nthFibonacci;
```
```