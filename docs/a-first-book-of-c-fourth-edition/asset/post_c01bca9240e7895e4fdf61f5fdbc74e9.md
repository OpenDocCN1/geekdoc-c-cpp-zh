
## Program 3.14

```
#include <iostream>
#include <iomanip>
using namespace std;

int main()
{
    const double SALESTAX = 0.05;
    double amount, taxes, total;

    cout << "\nEnter the amount purchased: ";
    cin >> amount;
    taxes = SALESTAX * amount;
    total = amount + taxes;
    cout << setiosflags(ios::fixed)
         << setiosflags(ios::showpoint)
         << setprecision(2);
    cout << "The sales tax is " << setw(4) << taxes << endl;
    cout << "The total bill is " << setw(5) << total << endl;

    return 0;
}
```

The following sample run was made with Program 3.14:

```
Enter the amount purchased: 36.00
The sales tax is 1.80
The total bill is 37.80
```

Although the const qualifier has been used to construct symbolic constants, you encounter this data type again in Chapter 11, where you learn that it's useful as a function argument to make sure the argument isn't modified in the function.

## EXERCISES 3.5

- 1. (Modify) Rewrite the following program to use the symbolic constant PI in place of the value 3.1416 used in the program:

```
#include <iostream>
using namespace std;
int main()
{
    double radius, circum;
```

```
cout << "Enter a radius: ";
cin >> radius;
circum = 2.0 * 3.1416 * radius;
cout << "\nThe circumference of the circle is "
<< circum << endl;

return 0;
}
```

- 2. (Modify) Rewrite the following program to use the named constant FACTOR in place of the expression (5.0/9.0) used in the program:

```
#include <iostream>
using namespace std;

int main()
{
    double fahren, celsius;
    cout << "Enter a temperature in degrees Fahrenheit: ";
    cin >> fahren;
    celsius = (5.0/9.0) * (fahren - 32.0);
    cout << "The equivalent Celsius temperature is "
    << celsius << endl;

    return 0;
}
```

- 3. (Modify) Rewrite the following program to use the symbolic constant PRIME in place of the value 0.04 used in the program:

```
#include <iostream>
using namespace std;

int main()
{
    double prime, amount, interest;
    prime = 0.04;    // prime interest rate
    cout << "Enter the amount: ";
    cin >> amount;
    interest = prime * amount;
    cout << "The interest earned is "
    << interest << " dollars" << endl;

    return 0;
}
```

- 4. (Program) Heat is radiated from the sun and all planets orbiting the sun. The heat that's radiated can be calculated by using the following formula:

E = ε σ T⁴

- E is the energy radiated per second in units of watts per meter squared (watts/m²).
- ε is the emissivity of the substance, which is 1 for the sun and all the planets.
- σ is the constant (.000000056697 = 5.6697e-8).
- T is the surface temperature in degrees Celsius.

For example, the heat radiated from the sun, which has an emissivity of 1 and a surface temperature of approximately 6000° C, is as follows:

E = (1) × (.000000056697) × (6000)⁴ watts/m²
= 73,479,300 watts/m²

Using the formula, write a C++ program that accepts a planet's temperature and provides the heat generated from the planet as its output. Your program should assign the value 5.6697e-8 to a symbolic constant named HEATFACTOR. After determining that your program is working correctly (make sure it produces the correct radiation for the sun), use it to complete the following chart:

| Planet (emissivity = 1) | Average Surface Temperature (° Celsius) | Heat Radiated (watts/m²) |
|---|---|---|
| Mercury | 270 | |
| Venus | 462 | |
| Earth | 14 | |

- 5. (Program) During the day, heat is absorbed by many objects, such as cars, roofs, and brick walls. This heat is then radiated back into the environment during the cooler evening hours. Using the formula E = ε σ T⁴ (see Exercise 4), write a C++ program that determines the amount of heat radiated for the objects listed in the following table. Your program should request the object's average surface temperature and emissivity, and then calculate and display the heat radiated. Make sure to use a symbolic constant named HEATFACTOR for the value of σ. Complete the following chart, making three runs of the program:

| Substance | Average Surface Temperature (° Celsius) | Emissivity | Heat Radiated (watts/m²) |
|---|---|---|---|
| Automobile | 47 | .3 | |
| Brick | 45 | .9 | |
| Commercial roof | 48 | .05 | |

## 3.6 Common Programming Errors

When using the material in this chapter, be aware of the following possible errors:

- 1. Forgetting to assign or initialize values for all variables before using them in an expression. Values can be assigned by assignment statements, initialized in a declaration statement, or assigned interactively by entering values with the cin object.
- 2. Using a mathematical library function without including the preprocessor statement #include <cmath> (and on a UNIX-based system, forgetting to include the -lm argument on the cc command line).
- 3. Using a library function without providing the correct number of arguments of the proper data type.
- 4. Applying the increment or decrement operator to an expression. For example, the expression (count + n)++ is incorrect. The increment and decrement operators can be applied only to variables.
- 5. Forgetting to use the extraction operator, >>, to separate variables in a cin statement.
- 6. A more unusual error occurs when increment and decrement operators are used with variables appearing more than once in the same expression. This error occurs because C++ doesn't specify the order in which operands are accessed in an expression. For example, the value assigned to result in the following statement depends on the compiler:
  
  result = i + i++;
  
  If your compiler accesses the first operand (i) first, the preceding statement is equivalent to
  
  result = 2 * i;
  i++;
  
  However, if your compiler accesses the second operand (i++) first, the value of the first operand is altered before it's used the second time, and the value 2i + 1 is assigned to result. As a general rule, don't use the increment or decrement operator in an expression when the variable it operates on appears more than once in the expression.
- 7. Being unwilling to test a program in depth. Being objective about testing your own software is difficult, but as a programmer, you must remind yourself that just because you think your program is correct doesn't make it so.

```
result = i + i++;
```

If your compiler accesses the first operand (i) first, the preceding statement is equivalent to

```
result = 2 * i;
i++;
```

However, if your compiler accesses the second operand (i++) first, the value of the first operand is altered before it's used the second time, and the value 2i + 1 is assigned to result. As a general rule, don't use the increment or decrement operator in an expression when the variable it operates on appears more than once in the expression.

## 3.7 Chapter Summary

- 1. An expression is a sequence of one or more operands separated by operators. An operand is a constant, a variable, or another expression. A value is associated with an expression.
- 2. Expressions are evaluated according to the precedence and associativity of the operators used in the expression.
- 3. The assignment operator is the = symbol. Expressions using this operator assign a value to a variable, and the expression also takes on a value. Because assignment is a C++ operation, the assignment operator can be used more than once in the same expression.
- 4. The increment operator, `++`, adds 1 to a variable, and the decrement operator, `--`, subtracts 1 from a variable. Both operators can be used as prefixes or postfixes. In a prefix operation, the variable is incremented (or decremented) before its value is used. In a postfix operation, the variable is incremented (or decremented) after its value is used.
- 5. C++ provides library functions for calculating square root, logarithmic, and other mathematical computations. Programs using a mathematical function must include the statement `#include <cmath>` or have a function declaration before calling the mathematical function.
- 6. Every mathematical library function operates on its arguments to calculate a single value. To use a library function effectively, you must know the function name, what the function does, the number and data types of arguments the function expects, and the data type of the returned value.
- 7. Data passed to a function is called an argument of the function. Arguments are passed to a library function by including each argument, separated by commas, in the parentheses following the function’s name. Each function has its own requirements for the number and data types of the arguments that must be provided.
- 8. Functions can be included in larger expressions.
- 9. The `cin` object is used for data input. It accepts a stream of data from the keyboard and assigns the data to variables. This is the general form of a statement using `cin`:

   `cin >> var1 >> var2 ... >> varn;`

   The extraction operator, `>>`, must be used to separate variable names in a `cin` statement.
- 10. When a `cin` statement is encountered, the computer temporarily suspends further execution until enough data has been entered for the number of variables in the `cin` statement.
- 11. It’s a good programming practice to display a message before a `cin` statement that alerts users to the type and number of data items to be entered. This message is called a prompt.
- 12. Values can be equated to a single constant by using the `const` keyword. This keyword creates a named constant that’s read-only after it’s initialized in the declaration statement. This declaration has the syntax

   `const dataType symbolicName = initialValue;`

   and permits using the constant instead of `initialValue` anywhere in the program after the declaration. Generally, these declarations are placed before variable declarations in a program.

## 3.8 Chapter Supplement: Errors, Testing, and Debugging

The ideal in programming is to produce readable, error-free programs that work correctly and can be modified or changed with a minimum of testing. You can work toward this ideal by keeping in mind the different types of errors that can occur, when they’re typically detected, and how to correct them.
