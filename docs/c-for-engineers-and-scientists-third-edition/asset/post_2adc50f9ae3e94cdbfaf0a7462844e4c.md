
## 330 Modularity Using Functions

Exchanging values in two variables is accomplished by using the three-step exchange algorithm:

- 1. Save the first parameter's value in a temporary location (see Figure 6.9a).
- 2. Store the second parameter's value in the first variable (see Figure 6.9b).
- 3. Store the temporary value in the second parameter (see Figure 6.9c).

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_349_0.png)

Figure 6.9a Save the first value

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_349_1.png)

Figure 6.9b Replace the first value with the second value

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_349_2.png)

Figure 6.9c Change the second value

Following is the swap() function written according to these specifications:

```cpp
void swap(double& num1, double& num2)
{
    double temp;

    temp = num1;      // save num1's value
    num1 = num2;      // store num2's value in num1
    num2 = temp;      // change num2's value

    return;
}
```

Notice the use of references in swap()'s header gives swap() access to equivalent arguments in the calling function. Therefore, any changes to the two reference parameters in swap() change the values in the calling function's arguments automatically. Program 6.10 contains swap() in a complete program.

## Chapter 6

## 331 Returning Multiple Values

### Program 6.10

```cpp
#include <iostream>
using namespace std;

void swap(double&a, double&b); // function receives two references

int main()
{
    double firstnum = 20.5, secnum = 6.25;

    cout << "The value stored in firstnum: " << firstnum << endl;
    cout << "The value stored in secnum: " << secnum << "\n\n";

    swap(firstnum, secnum); // call the function with references

    cout << "The value stored in firstnum is now: "
    << firstnum << endl;
    cout << "The value stored in secnum is now: "
    << secnum << endl;

    return 0;
}

void swap(double&num1, double&num2)
{
    double temp;
    temp = num1; // save num1's value
    num1 = num2; // store num2's value in num1
    num2 = temp; // change num2's value

    return;
}
```

The following is a sample run of Program 6.10:

The value stored in firstnum is: 20.5
The value stored in secnum is: 6.25

The value stored in firstnum is now: 6.25
The value stored in secnum is now: 20.5

As shown by Program 6.10's output, the values stored in main() variables are modified from within swap(), which was made possible by using reference parameters. If a pass by value had been used instead, the exchange in swap() would only affect swap()'s parameters and accomplish nothing with main()'s variables. A function as swap() can be written only by using a reference or some other means that provides access to main()'s variables. (This other means is with pointers, the topic of Chapter 12.)

In using reference, two cautions need to be mentioned. First, reference parameters must be by reference (that is, they can't be used to change constants). For example, calling swap() with two literals, in the call swap(20.5, 6.5), passes two constants to the function. However although swap () can execute, it doesn't change the values of these constants.

Second, a function call gives an indication that the return value will be by reference. In C++ this is done by reference rather than passes by reference, specifically limited to a called function(). This calling procedure should be adhered to whenever possible, which means reference parameters should be used only in restricted situations that require multiple return values, as in the swap () function in Program 6.10. The calc () function included in Program 6.9, although useful for illustration purposes, could be written as two separate functions, each returning a single value.

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_351_0.png)

## EXERCISES 6.3

- 1. (Practice) Write parameter declarations for the following:
   a. A parameter named *slope* that will be a reference to a double-precision value
   b. A parameter named *energy* that will be a reference to a double-precision number
   c. A parameter named *minutes* that will be a reference to an integer number
   d. A parameter named *key* that will be a reference to a character
   e. A parameter named *yield* that will be a reference to a double-precision number

- 2. (Practice) Three integer arguments are to be used in a call to a function named time(), assuming that time () accepts these variables as the reference parameters sec, min, and hours and returns value to its calling function.

- 3. (Modify) Rewrite the findMax() function in Program 6.5 so that the variable max, declared in main(), is used to store the maximum value of the two passed numbers. The value of max should be set from within findMax(Hint: A reference to max to be accepted by findMax().).

- 4. (Practice) Write a function named *change* that has an integer parameter and integer reference parameters named *hundreds*, *ifties*, *twenties*, *tens*, *fives*, and *ones*. The function is to consider the passed integer value as a dollar amount and return the value into the fewest number of equivalent bills. Using the reference parameters, the function should alter the arguments in the calling function.

- 5. (Practice) Write a function named *time* that has an integer parameter seconds and three integer reference parameters hours, mins, and secs. The...

> ¹³Most compilers catch this error.

## Chapter 6 333 A Case Study: Rectangular to Polar Coordinate Conversion

## 6.4 A Case Study: Rectangular to Polar Coordinate Conversion

Preparing a well-designed program is like preparing a paper, in that starts with an outline. This outline can be written down, for small programs, simply kept in mind. After the tasks are well defined, the actual work of coding can begin, in any order. If there are more tasks than one programmer can handle, they can be distributed among many programmers. This workload distribution is equivalent to having many people work on a large project, with each person responsible for a specific component. A general outline applicable to many engineering and scientific tasks is the following algorithm:

- Get the inputs to the problem
- Calculate the desired result
- Report the results of the calculation

These three tasks are the primary responsibilities of every program, and this algorithm is referred to as the problem-solver algorithm. Figure 6.10 shows a first-level structure diagram of this.

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_353_0.png)

**Figure 6.10** The problem-solver algorithm

### **Step 1** Problem Definition

A program is to be written to convert a point's rectangular (x,y) coordinates into polar form. That is, given an x and y position on a Cartesian coordinate system, shown in Figure 6.11, you must calculate the distance from the origin, $r$, and the angle from the x-axis, $	heta$, specified by the point. The values of $r$ and $	heta$ are referred to as the point's polar coordinates.

When the x and y coordinates of a point are known, the equivalent $r$ and $	heta$ coordinates can be calculated using these formulas:

```
$r = \sqrt{x^2 + y^2}$
$\theta = \tan^{-1}(y/x) \quad x \neq 0$
```

You begin developing your program with an outline of what the program is to accomplish. You can construct an initial pseudocode description by applying the problem-solver algorithm
