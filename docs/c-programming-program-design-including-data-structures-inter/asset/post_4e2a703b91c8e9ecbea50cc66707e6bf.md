
Recall that the extraction operator skips any leading whitespace characters and that reading stops at a whitespace character. As a consequence, you cannot use the extraction operator to read strings that contain blanks. For example, suppose that the variable name is defined as noted above. If the input is:

```text
Alice Wonderland
```

then after the statement:

```cpp
cin >> name;
```

executes, the value of the variable name is "Alice".

To read a string containing blanks, you can use the function getline.

The syntax to use the function getline is:

```cpp
getline(istreamVar, strVar);
```

where istreamVar is an input stream variable and strVar is a string variable. The reading is delimited by the newline character '\n'.

The function getline reads until it reaches the end of the current line. The newline character is also read but not stored in the string variable.

Consider the following statement:

```cpp
string myString;
```

If the input is 29 characters:

```text
bbbbHello there. How are you?
```

where b represents a blank, after the statement:

```cpp
getline(cin, myString);
```

the value of myString is:

```text
myString = "    Hello there. How are you?"
```

All 29 characters, including the first four blanks, are stored into myString.

Similarly, you can use an output stream variable, such as cout, and the insertion operator << to output the contents of a variable of the data type string.

## Debugging: Understanding Logic Errors and Debugging with cout Statements

In the debugging section of Chapter 2, we illustrated how to understand and correct syntax errors. As we have seen, syntax errors are reported by the compiler, and the compiler not only reports syntax errors, but also gives some explanation about the errors. On the other hand, logic errors are typically not caught by the compiler except for the trivial ones such as using a variable without properly initializing it. In this section, we illustrate how to spot and correct logic errors using cout statements. Suppose that we want to write a program that takes as input the temperature in Fahrenheit and outputs the equivalent temperature in Celsius. The formula to convert the temperature is: Celsius = 5 / 9 * (Fahrenheit − 32). So consider the following program:

```cpp
#include <iostream> //Line 1

using namespace std; //Line 2

int main() //Line 3
{
    int fahrenheit; //Line 5
    int celsius; //Line 6

    cout << "Enter temperature in Fahrenheit: "; //Line 7
    cin >> fahrenheit; //Line 8
    cout << endl; //Line 9

    celsius = 5 / 9 * (fahrenheit - 32); //Line 10

    cout << fahrenheit << " degree F = " //Line 11
         << celsius << " degree C." << endl;

    return 0; //Line 12
} //Line 13
```

**Sample Run 1:** In this sample run, the user input is shaded.

Enter temperature in Fahrenheit: **32**

32 degree F = 0 degree C.

**Sample Run 2:** In this sample run, the user input is shaded.

Enter temperature in Fahrenheit: **110**

110 degree F = 0 degree C.

The result shown in the first calculation looks correct. However, the result in the second calculation is clearly not correct even though the same formula is used, because 110 degree F = 43 degree C. It means the value of celsius calculated in Line 10 is incorrect. Now, the value of celsius is given by the expression 5 / 9 * (fahrenheit − 32). So we should look at this expression closely. To see the effect of this calculation, we can separately print the values of the two expressions 5 / 9 and fahrenheit − 32. This can be accomplished by temporarily inserting an output statement as shown in the following program:

```cpp
#include <iostream> //Line 1

using namespace std; //Line 2

int main() //Line 3
{
    int fahrenheit; //Line 5
    int celsius; //Line 6

    cout << "Enter temperature in Fahrenheit: "; //Line 7
    cin >> fahrenheit; //Line 8
    cout << endl; //Line 9

    cout << "5 / 9 = " << 5 / 9
         << "; fahrenheit - 32 = "
         << fahrenheit - 32 << endl; //Line 9a

    celsius = 5 / 9 * (fahrenheit - 32); //Line 10

    cout << fahrenheit << " degree F = "
         << celsius << " degree C. " << endl; //Line 11

    return 0; //Line 12
} //Line 13
```

**Sample Run:** In this sample run, the user input is shaded.

```text
Enter temperature in Fahrenheit: 110

5 / 9 = 0;  fahrenheit - 32 = 78
110 degree F = 0 degree C.
```

Let us look at the sample run. We see that the value of 5 / 9 = 0 and the value of fahrenheit - 32 = 78. Because fahrenheit = 110, the value of the expression fahrenheit - 32 is correct. Now let us look at the expression 5 / 9. The value of this expression is 0. Because both of the operands, 5 and 9, of the operator / are integers, using integer division, the value of the expression is 0. That is, the value of the expression 5 / 9 = 0 is also calculated correctly. So by the precedence of the operators, the value of the expression 5 / 9 * (fahrenheit - 32) will always be 0 regardless of the value of fahrenheit. So the problem is in the integer division. We can replace the expression 5 / 9 with 5.0 / 9. In this case, the value of the expression 5.0 / 9 * (fahrenheit - 32) will be a decimal number. Because fahrenheit and celsius are int variables, we can use the cast operators to convert this value to an integer, that is, we use the following expression:

```cpp
celsius = static_cast<int> (5.0 / 9 * (fahrenheit - 32) + 0.5);
```

(Note that in the preceding expression, we added 0.5 to round the number to the nearest integer.)

The revised program is:

```cpp
#include <iostream> //Line 1

using namespace std; //Line 2

int main() //Line 3
{
    int fahrenheit; //Line 4
    int celsius; //Line 5

    cout << "Enter temperature in Fahrenheit: "; //Line 7
    cin >> fahrenheit; //Line 8
    cout << endl; //Line 9

    celsius = static_cast<int>
              (5.0 / 9 * (fahrenheit - 32) + 0.5); //Line 10

    cout << fahrenheit << " degree F = "
         << celsius << " degree C." << endl; //Line 11

    return 0; //Line 12
} //Line 13
```

**Sample Run:** In this sample run, the user input is shaded.

Enter temperature in Fahrenheit: 110

110 degree F = 43 degree C.

As we can see, using temporary cout statements, we were able to find the problem. After correcting the problem, the temporary cout statements are removed.

The temperature conversion program contained logic errors, not syntax errors. Using cout statements to print the values of expressions and/or variables to see the results of a calculation is an effective way to find and correct logic errors.

## File Input/Output

The previous sections discussed in some detail how to get input from the keyboard (standard input device) and send output to the screen (standard output device). However, getting input from the keyboard and sending output to the screen have several limitations. Inputting data in a program from the keyboard is comfortable as long as the amount of input is very small. Sending output to the screen works well if the amount of data is small (no larger than the size of the screen) and you do not want to distribute the output in a printed format to others.

If the amount of input data is large, however, it is inefficient to type it at the keyboard each time you run a program. In addition to the inconvenience of typing large amounts of data, typing can generate errors, and unintentionally produce erroneous results. You must have some way to get data into the program from other sources. By using alternative sources of data, you can prepare the data before running a program, and the program can access the data each time it runs.

Suppose you want to present the output of a program in a meeting. Distributing printed copies of the program output is a better approach than showing the output on a screen. For example, you might give a printed report to each member of a committee before an important meeting. Furthermore, output must sometimes be saved so that the output produced by one program can be used as an input to other programs.

This section discusses how to obtain data from other input devices, such as a disk (that is, a secondary storage), and how to save the output to a disk. C++ allows a program to get
