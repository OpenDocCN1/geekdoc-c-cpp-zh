
# CHAPTER 5 The Selection Structure

HOW TO Use the fixed and scientific Stream Manipulators
Example 1
double sales = 10575.25;
cout << fixed;
cout << sales << endl;
Result displays 10575.250000

Example 2
double rate = 5.12345623;
cout << fixed << rate << endl;
displays 5.123456

Example 3
double rate = 5.12345693;
cout << fixed << rate << endl;
displays 5.123457

Example 4
double sales = 10575.25;
cout << scientific << sales << endl;
displays 1.05752e+004

Figure 5-25 How to use the fixed and scientific stream manipulators

Study the examples in Figure 5-25. Notice that the code in Example 1 displays 10575.250000 rather than 10575.25. This is because all numbers formatted by the fixed stream manipulator will have six digits to the right of the decimal point. If the unformatted number contains less than six decimal places, the fixed stream manipulator pads the number with zeros until it has six decimal places. The number 10575.25, for instance, is padded with four zeros to make it 10575.250000. If the unformatted number contains more than six decimal places, the additional decimal places are truncated (dropped off). Before the truncation, the number in the sixth decimal place is rounded up one number or left is, depending on the value of the numbers being truncated. For example, when the rate variable contains the number 5.12345623, it displays 5.123456. Notice that the digits 2 and 3, which occupy the seventh and eighth decimal places in the number 5.12345623, are truncated. Notice that the number in the sixth decimal place (6) remains the same as no rounding occurs because the value of the remaining numbers (23) is less than 50. However, when the rate variable contains the number 5.12345693, as it does in Example 3, the cout statement displays 5.123457. In this case, the digits in the seventh, eighth, and ninth decimal places (9, 3, and 2) are truncated. However, because the value of those numbers (932) is greater than 500, the number in the sixth decimal place (6) is rounded up to 7. The cout << scientific << sales << endl; statement in Example 4 displays the contents of the sales variable in e: the result is 1.05752e+004.

In most programs, especially business programs, output is displayed with either zero or two decimal places. Rarely does a program require numbers to be displayed with the six decimal places you get from the fixed stream manipulator. You can use the C++ setprecision stream manipulator definition of the setprecision manipulator is contained in the iomanip file, which comes with your C++ compiler. The "io" stands for "input/output". For a program to use the setprecision manipulator, it must contain the #include <iomanip>-directive. Figure 5-26 shows the setprecision manipulator's syntax. The numberDecimalPlaces argument is an integer that specifies the number of decimal places to include when displaying a real number. The setprecision manipulator remains effect until the end of the program or until the computer encounters another setprecision manipulator. Also included in Figure 5-26 are examples of using the setprecision manipulator in a C++ statement. As Example 2 shows, you can include the setprecision and fixed manipulators in the same statement.

> Stream manipulators with arguments (such as setprecision) are defined in the iomanip file. Stream manipulators that do not have arguments (such as fixed and scientific) are defined in the iostream file.

# HOW TO Use the setprecision Stream Manipulator

Syntax
setprecision(numberDecimalPlaces)

| Example 1 | Result |
| --- | --- |
| double sales = 3500.6;<br>cout << fixed;<br>cout << setprecision(2);<br>cout << sales << endl; | displays 3500.60 |
| Example 2 | |
| double rate = 10.0732;<br>cout << fixed << setprecision(3);<br>cout << rate << endl; | displays 10.073 |
| Example 3 | |
| double sales = 346.55;<br>cout << fixed;<br>cout << setprecision(0) << sales; | displays 347 |

Figure 5-26 How to use the setprecision manipulator

# Mini-Quiz 5-4

1. Which of the following tells the computer to display real numbers in fixed-point notation with two decimal places?
   a. cout << fixed << decimal(2);
   b. cout << fixed << precision(2);
   c. cout << fixed << precision(2);
   d. cout << fixed << setprecision(2);

2. Which of the following changes the contents of char named letter to lowercase?
   a. tolower(letter) = letter;
   b. letter == tolower(letter);
   c. letter = tolower(letter);
   d. tolower('letter');

> The answers to the Mini-Quiz are located in Appendix A.

3. If the num variable contains the number 34.65, the cout << fixed << num; statement will display the number as
   a. 34.65
   b. 34.650
   c. 34.600
   d. 34.65000

The answers to the labs are located in Appendix A.

# CHAPTER 5 The Selection Structure

LAB 5-1 Stop and Analyze

Study the program shown in Figure 5-27, and then answer the questions.

```cpp
//Lab5-1.cpp displays an employee's new salary
//Created/rev by <your name> on current date

#include <iostream>
#include <iomanip>
using namespace std;

int main() {
    double salary = 0.0;
    double rate = 0.0;
    char payGrade = ' ';

    cout << "Current salary: ";
    cin >> salary;
    cout << "Pay grade (1, 2, 3): ";
    cin >> payGrade;

    if (payGrade == '1')
        rate = .03;
    else
        rate = .02;

    salary = salary + salary * rate;
    cout << fixed << setprecision(2);
    cout << "New salary: " << salary << endl;

    system("pause");
    return 0;
} //end of main function
```

Figure 5-27 Program for Lab 5-1

# QUESTIONS

1. What rate be assigned to the rate variable when the user enters the following pay grades: 1, 3, and 5?
2. Why is the directive on Line 5 necessary?
3. Why is the 1 in the if statement's condition on Line 19 enclosed in quotation marks?
4. How would you rewrite the if statement on Lines 19 through 23 to use the != operator?
5. How else could you write the salary = salary * rate statement?
6. What changes would you need to make to the program so that it doesnt the rate variable?

# LAB 5-2 Plan and Create

In this lab, you will plan and create an algorithm for the manager of Willow Springs Health Club. The problem specification is shown in Figure 5-28.

> The manager of Willow Springs Health Club wants a program that allows her to enter the number of calories and fat contained in a specific food. The program should calculate and display two values: the food's calories and its percentage. The fat calories are the number of calories attributed to fat. The fat percentage is the ratio of the fat calories to its total calories. You can calculate a food's fat calories by multiplying its fat grams by the number 9, because each gram of fat contains 9 calories. To calculate the fat percentage, you divide the fat calories by its total calories and multiply the result by 100. The fat percentage should be displayed with zero decimal places. The program should display an appropriate error message if either or both input values are less than zero.

Figure 5-28 Problem Specification for Lab 5-2

First, analyze the problem, looking for the output first and for the input. In this case, the user wants the program to display a food's calories and its fat percentage. To calculate these values, the computer will need to know the food's total calories and its grams of fat; both of these items will be entered by the user. Next, plan the algorithm. As you know, most algorithms begin with instruction to enter the input items into the computer, followed by instructions that process the input items, typically including the items in one or more calculations. Most algorithms end with one or more instructions that display, print, or store the output items. Figure 5-29 shows the completed IPO chart for the health club.

# CHAPTER 5 The Selection Structure

| Input | Processing | Output |
|---|---|--|
| total calories | Processing items: none | fat calories |
| grams of fat | | fat percentage (decimal places) |

```
Algorithm:
1. enter the total calories and grams of fat
2. if (both the calories and grams of fat are greater than or equal zero)
   calculate fat calories by multiplying grams of fat by 9
   calculate fat percentage by dividing fat calories by total calories and then multiplying the result by 100
   display the fat calories and percentage
else
   display an error message
```

Figure 5-29 Completed IPO chart for the health club

After completing the IPO chart, you then move to the third step in the problem-solving process, you will desk the algorithm. For the first desk-desk, you will desk the health club algorithm three times. You will use 150 as the total calories and 6 as the grams of fat; the fat calories and fat percentage will be 54 and 36%, respectively. For the second desk-desk, you will use 105 as the total calories and 2 as the grams of fat. Using this data, the fat calories and fat percentage should be 18 and 17%, respectively. For the third desk-desk, you will use 100 as the total calories and -3 as the grams of fat. Using this data, the program should display an error message. Figure 5-30 shows the completed desk-desk table.

| total calories | grams of fat | fat calories | fat percentage |
|---|---|---|--|
| 150 | 6 | 54 | 36 |
| 105 | 2 | 18 | 17 |
| 100 | -3 | | |

Figure 5-30 Completed desk-desk table for the health club algorithm

The fourth step in the problem-solving process is to code the algorithm into a program. You begin by declaring memory locations that store the values of the input, (if any), and output items. The health club will need four memory locations to store the input and output items. The input items (total calories and grams of fat) will be stored in variables, because the user should be allowed to change the value of items during runtime. The output items (fat calories and fat percentage) also will be stored in variables, because their values are based on the current values of inputs. The total calories, grams of fat, and fat calories will
