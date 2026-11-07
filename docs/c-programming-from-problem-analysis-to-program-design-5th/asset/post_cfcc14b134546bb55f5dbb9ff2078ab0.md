
The following function implements this algorithm:

```cpp
bool isNumPalindrome(int num)
{
    int pwr = 0;

    if (num < 10)
        return true;                            //Step 1
    else                                        //Step 2
    {
        while (num / static_cast<int>(pow(10.0, pwr)) >= 10)   //Step 2.a
            pwr++;
        while (num >= 10)                       //Step 2.b
        {
            int tenToPwr = static_cast<int>(pow(10.0, pwr));

            if ((num / tenToPwr) != (num % 10))
                return false;                   //Step 2.b.1
            else                                //Step 2.b.2
            {
                num = num % tenToPwr;           //Step 2.b.2.1
                num = num / 10;                 //Step 2.b.2.1
                pwr = pwr - 2;                  //Step 2.b.2.2
            }
        }//end while

        return true;
    }//end else
}
```

> **NOTE**
>
> In the definition of the function isNumPalindrome, the function pow from the header file cmath is used to find the highest power of 10 that divides the number. Therefore, make sure to include the header file cmath in your program.

## Flow of Execution

As stated earlier, a C++ program is a collection of functions. Recall that functions can appear in any order. The only thing that you have to remember is that you must declare an identifier before you can use it. The program is compiled by the compiler sequentially from beginning to end. Thus, if the function main appears before any other user-defined functions, it is compiled first. However, if main appears at the end (or middle) of the program, all functions whose definitions (not prototypes) appear before the function main are compiled before the function main, in the order they are placed.

Function prototypes appear before any function definition, so the compiler translates these first. The compiler can then correctly translate a function call. However, when the program executes, the first statement in the function main always executes first, regardless of where in the program the function main is placed. Other functions execute only when they are called.

A function call statement transfers control to the first statement in the body of the function. In general, after the last statement of the called function executes, control is passed back to the point immediately following the function call. A value-returning function returns a value. Therefore, after executing the value-returning function, when the control goes back to the caller, the value that the function returns replaces the function call statement. The execution continues at the point immediately following the function call.

Suppose that a program contains functions funcA and funcB, and funcA contains a statement that calls funcB. Suppose that the program calls funcA. When the statement that contains a call to funcB executes, funcB executes, and while funcB is executing, the execution of the current call of funcA is on hold until funcB is done.

## PROGRAMMING EXAMPLE: Largest Number

In this programming example, the function larger is used to determine the largest number from a set of numbers. For the purpose of illustration, this program determines the largest number from a set of 10 numbers. You can easily enhance this program to accommodate any set of numbers.

**Input** A set of 10 numbers.  
**Output** The largest of 10 numbers.

### PROBLEM ANALYSIS AND ALGORITHM DESIGN

Suppose that the input data is:

15 20 7 8 28 21 43 12 35 3

Read the first number of the data set. Because this is the only number read to this point, you may assume that it is the largest number so far and call it max. Read the second number and call it num. Now compare max and num and store the larger number into max. Now max contains the larger of the first two numbers. Read the third number. Compare it with max and store the larger number into max. At this point, max contains the largest of the first three numbers. Read the next number, compare it with max, and store the larger into max. Repeat this process for each remaining number in the data set. Eventually, max will contain the largest number in the data set. This discussion translates into the following algorithm:

- 1. Read the first number. Because this is the only number that you have read so far, it is the largest number so far. Save it in a variable called `max`.
- 2. For each remaining number in the list:
  - a. Read the next number. Store it in a variable called num.
  - b. Compare num and max. If max < num, then num is the new largest number, so update the value of max by copying num into max. If max >= num, discard num; that is, do nothing.
- 3. Because max now contains the largest number, print it.

To find the larger of two numbers, the program uses the function larger.

### COMPLETE PROGRAM LISTING

```cpp
//**********************************************************
// Author: D.S. Malik
//
// This program finds the largest number of a set of 10
// numbers.
//**********************************************************

#include <iostream>

using namespace std;

double larger(double x, double y);

int main()
{
    double num; //variable to hold the current number
    double max; //variable to hold the larger number
    int count;  //loop control variable

    cout << "Enter 10 numbers." << endl;
    cin >> num;                         //Step 1
    max = num;                          //Step 1

    for (count = 1; count < 10; count++) //Step 2
    {
        cin >> num;                     //Step 2a
        max = larger(max, num);         //Step 2b
    }

    cout << "The largest number is " << max
         << endl;                       //Step 3
    return 0;
}//end main
```

```cpp
double larger(double x, double y)
{
    if (x >= y)
        return x;
    else
        return y;
}
```

Sample Run: In this sample run, the user input is shaded.

```text
Enter 10 numbers.
10 56 73 42 22 67 88 26 62 11
The largest number is 88
```

## PROGRAMMING EXAMPLE: Cable Company

Chapter 4 contains a program to calculate the bill for a cable company. In that program, all of the programming instructions are packed in the function main. Here, we rewrite the same program using user-defined functions, further illustrating structured programming. The program analysis phase shows how to divide a complex problem into smaller subproblems. It also shows that while solving a particular subproblem, you can focus on only that part of the program.

Input to and output of the program are the same as before.

### PROBLEM ANALYSIS AND ALGORITHM DESIGN

Because there are two types of customers, residential and business, the program contains two separate functions: one to calculate the bill for residential customers and one to calculate the bill for business customers. Both functions calculate the billing amount and then return the billing amount to the function main. The function main prints the amount due. Let us call the function that calculates the residential bill `residential` and the function that calculates the business bill `business`. The formulas to calculate the bills are the same as before.

As in Chapter 4, data such as the residential bill processing fee, the cost of residential basic service connection, and so on are special. Therefore, these are declared as named constants.

### Function `residential`

To compute the residential bill, you need to know the number of premium channels to which the customer subscribes. Based on the number of premium channels, you can calculate the billing amount. After calculating the billing amount, the function returns the billing amount using the `return` statement. The following four steps describe this function:

- a. Prompt the user for the number of premium channels.
- b. Read the number of premium channels.
- c. Calculate the bill.
- d. Return the amount due.

This function contains a statement to prompt the user to enter the number of premium channels (Step a) and a statement to read the number of premium channels (Step b). Other items needed to calculate the billing amount, such as the cost of basic service connection and bill-processing fees, are defined as named constants (before the definition of the function main). Therefore, to calculate the billing amount, this function does not need to get any value from the function main. This function, therefore, has no parameters.

### Local Variables (Function residential)

From the previous discussion, it follows that the function residential requires variables to store both the number of premium channels and the billing amount. This function needs only two local variables to calculate the billing amount:

```cpp
int noOfPChannels;   //number of premium channels
double bAmount;      //billing amount
```

The definition of the function residential can now be written as follows:

```cpp
double residential()
{
    int noOfPChannels;   //number of premium channels
    double bAmount;      //billing amount
    cout << "Enter the number of premium "
         << "channels used: ";
    cin >> noOfPChannels;
    cout << endl;

    bAmount = RES_BILL_PROC_FEES +
              RES_BASIC_SERV_COST +
              noOfPChannels * RES_COST_PREM_CHANNEL;

    return bAmount;
}
```

### Function business

To compute the business bill, you need to know the number of both the basic service connections and the premium channels to which the customer subscribes. Then, based on these numbers, you can calculate the billing amount. The billing amount is then returned using the return statement. The following six steps describe this function:

- a. Prompt the user for the number of basic service connections.
- b. Read the number of basic service connections.
- c. Prompt the user for the number of premium channels.
- d. Read the number of premium channels.
- e. Calculate the bill.
- f. Return the amount due.
