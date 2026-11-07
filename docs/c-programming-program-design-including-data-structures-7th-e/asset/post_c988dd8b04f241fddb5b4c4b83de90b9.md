
- 44. If a formal parameter needs to change the value of an actual parameter, in the function heading, you must declare this formal parameter as a reference parameter.
- 45. The scope of an identifier refers to those parts of the program where it is accessible.
- 46. Variables declared within a function (or block) are called local variables.
- 47. Variables declared outside of every function definition (and block) are called global variables.
- 48. The scope of a function name is the same as the scope of an identifier declared outside of any block.
- 49. See the scope rules in this chapter (see the section, Scope of an Identifier).
- 50. C++ does not allow the nesting of function definitions.
- 51. An automatic variable is a variable for which memory is allocated on function (or block) entry and deallocated on function (or block) exit.
- 52. A static variable is a variable for which memory remains allocated throughout the execution of the program.
- 53. By default, global variables are static variables.
- 54. In C++, a function can be overloaded.
- 55. Two functions are said to have different formal parameter lists if both functions have:
  - A different number of formal parameters, or
  - The same number of formal parameters and the data types of the formal parameters, in the order listed, differ in at least one position.
- 56. The signature of a function consists of the function name and its formal parameter list. Two functions have different signatures if they have either different names or different formal parameter lists.
- 57. If a function is overloaded, then, in a call to that function the formal parameter list of the function determines which function to execute.
- 58. C++ allows functions to have default parameters.
- 59. If you do not specify the value of a default parameter, the default value is used for that parameter.
- 60. All of the default parameters must be the far-right parameters of the function.
- 61. Suppose a function has more than one default parameter. In a function call, if a value to a default parameter is not specified, then you must omit all arguments to its right.
- 62. Default values can be constants, global variables, or function calls.
- 63. The calling function has the option of specifying a value other than the default for any default parameter.
- 64. You cannot assign a constant value as a default value to a reference parameter.

![](img/d0be7fc6d804b63484835c6c8bc67a07_485_0.png)

## EXERCISES

The number in parentheses at the end of an exercise refers to the learning objective listed at the beginning of the chapter.

- 1. Mark the following statements as true or false:
  - a. To use a predefined function in a program, you need to know only the name of the function and how to use it. (1)
  - b. A value-returning function returns only one value. (2, 3)
  - c. Parameters allow you to use different values each time the function is called. (2, 7, 9)
  - d. When a `return` statement executes in a user-defined function, the function immediately exits. (3, 4)
  - e. A value-returning function returns only integer values. (4)
  - f. A variable name cannot be passed to a value parameter. (3, 6)
  - g. If a C++ function does not use parameters, parentheses around the empty parameter list are still required. (2, 3, 6)
  - h. In C++, the names of the corresponding formal and actual parameters must be the same. (3, 4, 6)
  - i. A function that changes the value of a reference parameter also changes the value of the actual parameter. (7)
  - j. Whenever the value of a reference parameter changes, the value of the actual parameter changes. (7)
  - k. In C++, function definitions can be nested; that is, the definition of one function can be enclosed in the body of another function. (9)
  - l. Using global variables in a program is a better programming style than using local variables, because extra variables can be avoided. (10)
  - m. In a program, global constants are as dangerous as global variables. (10)
  - n. The memory for a static variable remains allocated between function calls. (11)

- 2. Determine the value of each of the following expressions: (1)
  - a. `static_cast<char>(toupper('7'))`
  - b. `static_cast<char>(toupper('@'))`
  - c. `static_cast<char>(toupper('s'))`
  - d. `static_cast<char>(toupper('J'))`
  - e. `static_cast<char>(tolower('*'))`
  - f. `static_cast<char>(tolower(';'))`
  - g. `static_cast<char>(tolower('W'))`
  - h. `static_cast<char>(tolower('('))`

- 3. Determine the value of each of the following expressions. (For decimal numbers, round your answer to two decimal places.) (1)
  - a. abs(-25)
  - b. fabs(-56.38)
  - c. fabs(13.00)
  - d. pow(3.0, 2)
  - e. pow(6.2, 1.5)
  - f. sqrt(34.56)
  - g. sqrt(144.0)
  - h. sqrt(49.00) * pow(6.0, 3.0) / abs(-3)
  - i. floor(13.45)
  - j. ceil(6.5)
  - k. floor(5.89) + ceil(5.89)
  - l. floor(-5.89) + ceil(-2.31)
  - m. floor(-2.3) - ceil(81.2)
  - n. pow(-3.0, 5.0)
  - o. pow(3.0, -5.0)
  - p. pow(4.2, 1/5.0)

- 4. Using the functions described in Table 6-1, write each of the following as a C++ expression. (The expression in (e) denotes the absolute value of x + 2y - 3.) (1)
  - a. 8.5^3.2
  - b. sqrt(3x^2 - y)
  - c. (u+w)^(2x)
  - d. (-b + sqrt(b^2 - 4ac))/(2a)
  - e. |x + 2y - 3|

- 5. Consider the following function definition:

```cpp
int func(int x, double y, char u, string name)
{
    //function body
}
```

Which of the following are correct function prototypes of the function func? (4, 6)

  - a. int func(x, y, u, name);
  - b. int func(int s, double k, char ch, string name);
  - c. int func(int, double, char, string);
  - d. func(int, double, char, string)

- 6. Consider the following program: (1)

```cpp
#include <iostream>
#include <cmath>
#include <iomanip>

using namespace std;

int main()
{
    int num1;
    int num2;

    cout << fixed << showpoint << setprecision(2);

    cout << "Enter two integers: ";
    cin >> num1 >> num2;
    cout << endl;

    if (num1 != 0 && num2 != 0)
        cout << sqrt(abs(num1 + num2) + 0.5) << endl;
    else if (num1 != 0)
        cout << floor(num1 + 0.5) << endl;
    else if (num2 != 0)
        cout << ceil(num2 + 0.5) << endl;
    else
        cout << 0 << endl;

    return 0;
}
```

  - a. What is the output if the input is -23 8?
  - b. What is the output if the input is 12 32?
  - c. What is the output if the input is 15 0?
  - d. What is the output if the input is 0 -36?
  - e. What is the output if the input is 0 0?

- 7. Consider the following statements:

```cpp
int num1, num2, num3;
double length, width, height;
double volume;
num1 = 6; num2 = 7; num3 = 4;
length = 6.2; width = 2.3; height = 3.4;
```

and the function prototype:

```cpp
double box(double, double, double);
```

Which of the following statements are valid? If they are invalid, explain why. (4)

  - a. volume = box(length, width, height);
  - b. volume = box(length, 3.8, height);
  - c. cout << box(num1, num2) << endl;
  - d. cout << box(length, width, 7.0) << endl;
  - e. volume = box(length, num1, height);
  - f. cout << box(6.2, height) << endl;
  - g. volume = box(length + width, height);
  - h. volume = box(num1, num2 + num3);

- 8. Consider the following functions: (4)

```cpp
int find(int num1, int num2)
{
    int first, second;

    first = num1 * num2;
    second = first - num1 + num2;

    if (second > 50)
        num1 = first / 10;
    else
        num2 = second / 20;

    return num1 + num2;
}

int discover(int one, int two)
{
    int secret = 1;
    for (int i = one; i < two; i++)
        secret = secret * i;

    return secret;
}
```

What is the output of each of the following program segments?

  - a. `cout << find(15, 25) << endl;`
  - b. `cout << discover(3, 9) << endl;`
  - c. `cout<<find(10, 10)<<" "<<discover(10, find(10, 10))<<endl;`
  - d. `x = 20; y = 10;` `cout << discover(x, y) << endl;`

- 9. Consider the following function prototypes:

```cpp
int func1(int, double);
double func2(string, int, double);
char func3(int, int, double, char);
string join(string, string);
```

Answer the following questions: (3, 4)

  - a. How many parameters does the function func1 have? What is the type of the function func1?
  - b. How many parameters does function func2 have? What is the type of the function func2?
  - c. How many parameters does function func3 have? What is the type of function func3?
  - d. How many parameters does the function join have? What is the type of function join?
  - e. How many actual parameters are needed to call the function func1? What is the type of each actual parameter, and in what order should you use these parameters in a call to the function func1?
  - f. Write a C++ statement that prints the value returned by the function func1 with the actual parameters 3 and 8.5.

