
Your program should allow the user to enter any date and output the corresponding day of the week in English.

## 13.

You have four identical prizes to give away and a pool of 25 finalists. The finalists are assigned numbers from 1 to 25. Write a program to randomly select the numbers of 4 finalists to receive a prize. Make sure not to pick the same number twice. For example, picking finalists 3, 15, 22, and 14 would be valid but picking 3, 3, 31, and 17 would be invalid, because finalist number 3 is listed twice and 31 is not a valid finalist number.

## 14.

Programming Project 2.9 asked you to implement the Babylonian Algorithm to compute the square root of a number. Put this algorithm into a function and test it by using it to calculate the square root of several numbers. The function should return the square root as a double and also process the number n as a double.

## 15.

The Social Security Administration maintains an actuarial life table that contains the probability that a person in the United States will die (http://www.ssa.gov/OACT/STATS/table4c6.html). The death probabilities for 2009 are stored in the file LifeDeathProbability.txt, which is included on the website for the book. There are three values for each row: the age, the death probability for a male, and the death probability for a female. For example, the first five lines are

```
0 0.006990 0.005728
1 0.000447 0.000373
2 0.000301 0.000241
3 0.000233 0.000186
4 0.000177 0.000150
```

The interpretation for the fourth line is that a 3-year-old female has a 0.000186 chance of dying during year 3 to 4.

Write a program that inputs an age and sex from the keyboard in the main function. The main function should call a function named simulate (that you must write), sending in the age and sex as parameters. The function should simulate to what age a person will live by starting with the death probability for the given age and sex. You can do this by reading the data from the file row by row. Skip rows that are less than the input age. Once the input age is reached, generate a random number between 0 and 1, and if this number is less than or equal to the corresponding death probability, then predict that the person will live to the current age and return that age. If the random number is greater than the death probability, then increase the age by one and repeat the calculation for the next row in the file. If the simulation reaches age 120, then stop and predict that the user will live to 120. The main function should output the simulated age at which the person will die. This program is merely a simulation and will give different results each time it is run, assuming you change the seed for the random number generator.

## Parameters and Overloading 4

### 4.1 PARAMETERS 176

Call-by-Value Parameters 176

A First Look at Call-by-Reference Parameters 178

Call-by-Reference Mechanism in Detail 181

Constant Reference Parameters 183

Example: The swapValues Function 183

Tip: Think of Actions, Not Code 184

Mixed Parameter Lists 185

Tip: What Kind of Parameter to Use 186

Pitfall: Inadvertent Local Variables 188

Tip: Choosing Formal Parameter Names 189

Example: Buying Pizza 190

### 4.2 OVERLOADING AND DEFAULT ARGUMENTS 193

Introduction to Overloading 193

Pitfall: Automatic Type Conversion and Overloading 196

Rules for Resolving Overloading 197

Example: Revised Pizza-Buying Program 199

Default Arguments 201

### 4.3 TESTING AND DEBUGGING FUNCTIONS 203

The assert Macro 203

Stubs and Drivers 204

## 4 Parameters and Overloading

Just fill in the blanks.

Common instruction

# Introduction

This chapter discusses the details of the mechanisms used by C++ for plugging in arguments for parameters in function calls. It also discusses overloading, which is a way to give two (or more) different function definitions to the same function name. Finally, it goes over some basic techniques for testing functions.

## 4.1 Parameters

You can't put a square peg in a round hole.

Common saying

This section describes the details of the mechanisms used by C++ for plugging in an argument for a formal parameter when a function is invoked. There are two basic kinds of parameters and therefore two basic plugging-in mechanisms in C++. The two basic kinds of parameters are call-by-value parameters and call-by-reference parameters. All the parameters that appeared before this point in the book were call-by-value parameters.

With call-by-value parameters, only the value of the argument is plugged in. With call-by-reference parameters, the argument is a variable, and the variable itself is plugged in; therefore, the variable's value can be changed by the function invocation. A call-by-reference parameter is indicated by appending the ampersand sign, &, to the parameter type, as illustrated by the following function declarations:

```
void getInput(double& variableOne, int& variableTwo);
```

A call-by-value parameter is indicated by not using the ampersand. The details on call-by-value and call-by-reference parameters are given in the following subsections.

## Call-by-Value Parameters

Call-by-value parameters are more than just blanks that are filled in with the argument values for the function. A call-by-value parameter is actually a local variable. When the function is invoked, the value of a call-by-value argument is computed, and the corresponding call-by-value parameter, which is a local variable, is initialized to this value.

In most cases, you can think of a call-by-value parameter as a kind of blank, or placeholder, that is filled in by the value of its corresponding argument in the function invocation. However, in some cases it is handy to use a call-by-value parameter as a local variable and change the value of the parameter within the body of the function

call-by-value parameter

call-by-reference parameter

definition. For example, the program in Display 4.1 illustrates a call-by-value parameter used as a local variable whose value is changed in the body of the function definition. Notice the formal parameter minutesWorked in the definition of the function fee. It is used as a variable and has its value changed by the following line, which occurs within the function definition:

```
minutesWorked = hoursWorked*60 + minutesWorked;
```

## Display 4.1 Formal Parameter Used as a Local Variable (part 1 of 2)

```
//Law office billing program.
#include <iostream>
using namespace std;

const double RATE = 150.00; //Dollars per quarter hour.

double fee(int hoursWorked, int minutesWorked);
//Returns the charges for hoursWorked hours and
//minutesWorked minutes of legal services.

int main()
{
    int hours, minutes;
    double bill;

    cout << "Welcome to the law office of\n"
         << "Dewey, Cheatham, and Howe.\n"
         << "The law office with a heart.\n"
         << "Enter the hours and minutes"
         << " of your consultation:\n";
    cin >> hours >> minutes;

    bill = fee(hours, minutes);

    cout.setf(ios::fixed);
    cout.setf(ios::showpoint);
    cout.precision(2);
    cout << "For " << hours << " hours and " << minutes
         << " minutes, your bill is $" << bill << endl;

    return 0;
}
double fee(int hoursWorked, int minutesWorked)
{
    int quarterHours;

    minutesWorked = hoursWorked*60 + minutesWorked;
    quarterHours = minutesWorked/15;
    return (quarterHours*RATE);
}
```

The value of minutes is not changed by the call to fee.

minutesWorked is a local variable initialized to the value of minutes.

## Display 4.1 Formal Parameter Used as a Local Variable (part 2 of 2)

# Sample Dialogue

```
Welcome to the law office of
Dewey, Cheatham, and Howe.
The law office with a heart.
Enter the hours and minutes of your consultation:
5 46
For 5 hours and 46 minutes, your bill is $3450.00
```

Call-by-value parameters are local variables just like the variables you declare within the body of a function. However, you should not add a variable declaration for the formal parameters. Listing the formal parameter minutesWorked in the function heading also serves as the variable declaration. The following is the wrong way to start the function definition for fee because it declares minutesWorked twice:

```
double fee(int hoursWorked, int minutesWorked)
{
    int quarterHours;
    int minutesWorked;
    ...
```

Do not do this when minutesWorked is a parameter!

## Self-Test Exercises

- 1. Carefully describe the call-by-value parameter mechanism.
- 2. The following function is supposed to take as arguments a length expressed in feet and inches and to return the total number of inches in that many feet and inches. For example, totalInches(1, 2) is supposed to return 14, because 1 foot and 2 inches is the same as 14 inches. Will the following function perform correctly? If not, why not?

```
double totalInches(int feet, int inches)
{
    inches = 12*feet + inches;
    return inches;
}
```

## A First Look at Call-by-Reference Parameters

The call-by-value mechanism that we used until now is not sufficient for all tasks you might want a function to perform. For example, one common task for a function is to obtain an input value from the user and set the value of an argument variable to this input value. With the call-by-value formal parameters that we have used until now, a
