# EXAMPLE 5-16 (FIBONACCI NUMBER PROGRAM: REVISITED)

The Programming Example: Fibonacci Number given in the previous section uses a `while` loop to determine the desired Fibonacci number. You can replace the `while` loop with an equivalent `for` loop as follows:

```
for (counter = 3; counter <= nthFibonacci; counter++)
{
    current = previous2 + previous1;
    previous1 = previous2;
    previous2 = current;
}//end for
```

The complete program listing of the program that uses a `for` loop to determine the desired Fibonacci number is given at the website accompanying this book. The program is named `Ch5_FibonacciNumberUsingAForLoop.cpp`.

In the following C++ program, we recommend that you walk-through each step.

# EXAMPLE 5-17

The following C++ program finds the sum of the first n positive integers.

```
//Program to determine the sum of the first n positive numbers.

#include <iostream>                                      //Line 1

using namespace std;                                     //Line 2

int main()                                                //Line 3
{
    int counter; //loop control variable                  //Line 5
    int sum;     //variable to store the sum of numbers   //Line 6
    int N;       //variable to store the number of       //Line 7
                //first positive integers to be added

    cout << "Line 8: Enter the number of positive "
         << "integers to be added: ";                    //Line 8
    cin >> N;                                             //Line 9
    sum = 0;                                              //Line 10
    cout << endl;                                         //Line 11

    for (counter = 1; counter <= N; counter++)            //Line 12
        sum = sum + counter;                              //Line 13

    cout << "Line 14: The sum of the first " << N
         << " positive integers is " << sum
         << endl;                                         //Line 14

    return 0;                                             //Line 15
}                                                        //Line 16
```