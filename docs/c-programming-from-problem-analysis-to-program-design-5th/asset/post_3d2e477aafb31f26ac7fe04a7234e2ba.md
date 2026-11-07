
```cpp
cout << first << " " << last << " today's temperature is: ";
    << temperature << endl;

return 0;
}
```

- 25. What action must be taken before a variable can be used in a program?

- 26. Preprocessor directives begin with which of the following symbols:
  - a. `*`
  - b. `#`
  - c. `$`
  - d. `!`
  - e. None of these.

- 27. Write equivalent compound statements if possible.
  - a. `x = 2 * x`
  - b. `x = x + y - 2;`
  - c. `sum = sum + num;`
  - d. `z = z * x + 2 * z;`
  - e. `y = y / (x + 5);`

- 28. Write the following compound statements as equivalent simple statements.
  - a. `x += 5 - z;`
  - b. `y *= 2 * x + 5 - z;`
  - c. `w += 2 * z + 4;`
  - d. `x -= z + y - t;`
  - e. `sum += num;`

- 29. Suppose a, b, and c are int variables and a = 5 and b = 6. What value is assigned to each variable after each statement executes? If a variable is undefined at a particular statement, report UND (undefined).

| Statement | a | b | c |
|---|---:|---:|---:|
| `a = (b++) + 3;` | — | — | — |
| `c = 2 * a + (++b);` | — | — | — |
| `b = 2 * (++c) - (a++);` | — | — | — |

- 30. Suppose a, b, and sum are int variables and c is a double variable. What value is assigned to each variable after each statement executes? Suppose a = 3, b = 5, and c = 14.1.

| Statement | a | b | c | sum |
|---|---:|---:|---:|---:|
| `sum = a + b + c;` | — | — | — | — |
| `c /= a;` | — | — | — | — |
| `a += c - a;` | — | — | — | — |
| `a *= 2 * b + c;` | — | — | — | — |

- 31. What is printed by the following program? Suppose the input is:

`20 15`

```cpp
#include <iostream>

using namespace std;

const int NUM = 10;
const double X = 20.5;

int main()
{
    int a, b;
    double z;
```

- 4. Repeat Exercise 3 by declaring num1, num2, and num3, and average of type double. Store 75.35 into num1, -35.56 into num2, and 15.76 into num3.

- 5. Consider the following C++ program in which the statements are in the incorrect order. Rearrange the statements so that it prompts the user to input the length and width of a rectangle and output the area and perimeter of the rectangle.

```cpp
#include <iostream>
{
    int main()

    cout << "Enter the length: ";
    cin >> length;
    cout << endl;

    int length;

    area = length * width;

    return 0;

    int width;

    cin >> width;
    cout << "Enter the width: ";
    cout << endl;

    cout << "Area = " << area << endl;
    cout << "Perimeter = " << perimeter << endl;

    int area;
    using namespace std;
    int perimeter;
}
```

- 6. Consider the following program segment:

```cpp
//include statement(s)
//using namespace statement

int main()
{
    //variable declaration

    //executable statements

    //return statement
}
```

  - a. Write C++ statements that include the header files `iostream` and `string`.
  - b. Write a C++ statement that allows you to use `cin`, `cout`, and `endl` without the prefix `std::`.
  - c. Write C++ statements that declare the following variables: name of type `string` and studyHours of type `double`.
  - d. Write C++ statements that prompt and input a string into `name` and a `double` value into `studyHours`.
  - e. Write a C++ statement that outputs the values of `name` and `studyHours` with the appropriate text. For example, if the value of `name` is "Donald" and the value of `studyHours` is 4.5, the output is:

Hello, Donald! On Saturday, you need to study 4.5 hours for the exam.

  - f. Compile and run your program.

- 7. Write a program that prompts the user to input a decimal number and outputs the number rounded to the nearest integer.

- 8. Consider the following program segment:

```cpp
//include statement(s)
//using namespace statement

int main()
{
    //variable declaration

    //executable statements

    //return statement
}
```

  - a. Write C++ statements that include the header files `iostream` and `string`.
  - b. Write a C++ statement that allows you to use `cin`, `cout`, and `endl` without the prefix `std::`.
  - c. Write C++ statements that declare and initialize the following named constants: SECRET of type `int` initialized to 11 and RATE of type `double` initialized to 12.50.
  - d. Write C++ statements that declare the following variables: `num1`, `num2`, and `newNum` of type `int`; `name` of type `string`; and `hoursWorked` and `wages` of type `double`.
  - e. Write C++ statements that prompt the user to input two integers and store the first number in `num1` and the second number in `num2`.
  - f. Write a C++ statement(s) that outputs the values of num1 and num2, indicating which is num1 and which is num2. For example, if num1 is 8 and num2 is 5, then the output is:

The value of num1 = 8 and the value of num2 = 5.

  - g. Write a C++ statement that multiplies the value of num1 by 2, adds the value of num2 to it, and then stores the result in newNum. Then, write a C++ statement that outputs the value of newNum.
  - h. Write a C++ statement that updates the value of newNum by adding the value of the named constant SECRET. Then, write a C++ statement that outputs the value of newNum with an appropriate message.
  - i. Write C++ statements that prompt the user to enter a person’s last name and then store the last name into the variable name.
  - j. Write C++ statements that prompt the user to enter a decimal number between 0 and 70 and then store the number entered into hoursWorked.
  - k. Write a C++ statement that multiplies the value of the named constant RATE with the value of hoursWorked and then stores the result into the variable wages.
  - l. Write C++ statements that produce the following output:

```cpp
Name:          //output the value of the variable name
Pay Rate: $    //output the value of the variable rate
Hours Worked:  //output the value of the variable hoursWorked

Salary: $      //output the value of the variable wages
```

For example, if the value of name is "Rainbow" and hoursWorked is 45.50, then the output is:

```cpp
Name: Rainbow
Pay Rate: $12.50
Hours Worked: 45.50
Salary: $568.75
```

  - m. Write a C++ program that tests each of the C++ statements that you wrote in parts a through l. Place the statements at the appropriate place in the previous C++ program segment. Test run your program (twice) on the following input data:
    - a. num1 = 13, num2 = 28; name = "Jacobson"; hoursWorked = 48.30.
    - b. num1 = 32, num2 = 15; name = "Crawford"; hoursWorked = 58.45.

- 9. Write a program that prompts the user to enter five test scores and then prints the average test score. (Assume that the test scores are decimal numbers.)

- 10. Write a program that prompts the user to input five decimal numbers. The program should then add the five decimal numbers, convert the sum to the nearest integer, and print the result.

- 11. Write a program that does the following:
  - a. Prompts the user to input five decimal numbers.
  - b. Prints the five decimal numbers.
  - c. Converts each decimal number to the nearest integer.
  - d. Adds the five integers.
  - e. Prints the sum and average of the five integers.

- 12. Write a program that prompts the capacity, in gallons, of an automobile fuel tank and the miles per gallons the automobile can be driven. The program outputs the number of miles the automobile can be driven without refueling.

- 13. Write a C++ program that prompts the user to input the elapsed time for an event in seconds. The program then outputs the elapsed time in hours, minutes, and seconds. (For example, if the elapsed time is 9630 seconds, then the output is 2:40:30.)

- 14. Write a C++ program that prompts the user to input the elapsed time for an event in hours, minutes, and seconds. The program then outputs the elapsed time in seconds.

- 15. To make a profit, a local store marks up the prices of its items by a certain percentage. Write a C++ program that reads the original price of the item sold, the percentage of the marked-up price, and the sales tax rate. The program then outputs the original price of the item, the percentage of the mark-up, the store's selling price of the item, the sales tax rate, the sales tax, and the final price of the item. (The final price of the item is the selling price plus the sales tax.)

- 16. Write a program that prompts the user to input a length expressed in centimeters. The program should then convert the length to inches (to the nearest inch) and output the length expressed in yards, feet, and inches, in that order. For example, suppose the input for centimeters is 312. To the nearest inch, 312 centimeters is equal to 123 inches. 123 inches would thus be output as:

3 yard(s), 1 feet (foot), and 3 inch(es).

- 17. Write a program to implement and test the algorithm that you designed for Exercise 15 of Chapter 1. (You may assume that the value of π = 3.141593. In your program, declare a named constant PI to store this value.)

- 18. A milk carton can hold 3.78 liters of milk. Each morning, a dairy farm ships cartons of milk to a local grocery store. The cost of producing one liter of milk is $0.38, and the profit of each carton of milk is $0.27. Write a program that does the following:
