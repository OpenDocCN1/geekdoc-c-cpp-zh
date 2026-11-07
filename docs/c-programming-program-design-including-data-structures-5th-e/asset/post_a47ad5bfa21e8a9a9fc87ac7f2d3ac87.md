
correct logic errors using cout statements. Suppose that we want to write a program that takes as input the temperature in Fahrenheit and outputs the equivalent temperature in Celsius. The formula to convert the temperature is: Celsius = 5 / 9 * (Fahrenheit - 32). So consider the following program:

```cpp
#include <iostream>                                      //Line 1

using namespace std;                                     //Line 2

int main()                                               //Line 3
{                                                        //Line 4
    int fahrenheit;                                      //Line 5
    int celsius;                                         //Line 6

    cout << "Enter temperature in Fahrenheit: ";         //Line 7
    cin >> fahrenheit;                                   //Line 8
    cout << endl;                                        //Line 9

    celsius = 5 / 9 * (fahrenheit - 32);                 //Line 10

    cout << fahrenheit << " degree F = "
         << celsius << " degree C. " << endl;            //Line 11

    return 0;                                            //Line 12
}                                                        //Line 13
```

**Sample Run 1**: In this sample run, the user input is shaded.

Enter temperature in Fahrenheit: 32

32 degree F = 0 degree C.

**Sample Run 2**: In this sample run, the user input is shaded.

Enter temperature in Fahrenheit: 110

110 degree F = 0 degree C.

The result shown in the first calculation looks correct. However, the result in the second calculation is clearly not correct even though the same formula is used, because 110 degree F = 43 degree C. It means the value of Celsius calculated in Line 10 is incorrect. Now, the value of Celsius is given by the expression 5 / 9 * (fahrenheit - 32). So we should look at this expression closely. To see the effect of this expression, we can separately print the values of the two expressions 5 / 9 and fahrenheit - 32. This can be accomplished by temporarily inserting an output statement as shown in the following program:

```cpp
#include <iostream>                                      //Line 1

using namespace std;                                     //Line 2

int main()                                               //Line 3
{                                                        //Line 4
    int fahrenheit;                                      //Line 5
    int celsius;                                         //Line 6

    cout << "Enter temperature in Fahrenheit: ";  //Line 7
    cin >> fahrenheit;                            //Line 8
    cout << endl;                                 //Line 9

    cout << "5 / 9 = " << 5 / 9
         << "; fahrenheit - 32 = "
         << fahrenheit - 32 << endl;              //Line 9a

    celsius = 5 / 9 * (fahrenheit - 32);          //Line 10

    cout << fahrenheit << " degree F = "
         << celsius << " degree C. " << endl;     //Line 11

    return 0;                                      //Line 12
}                                                  //Line 13
```

**Sample Run:** In this sample run, the user input is shaded.

```
Enter temperature in Fahrenheit: 110

5 / 9 = 0; fahrenheit - 32 = 78
110 degree F = 0 degree C.
```

Let us look at the sample run. We see that the value of 5 / 9 = 0 and the value of fahrenheit - 32 = 78. Because fahrenheit = 110, the value of the expression fahrenheit - 32 is correct. Now let us look at the expression 5 / 9. The value of this expression is 0. Because both of the operands, 5 and 9, of the operator / are integers, using integer division, the value of the expression is 0. That is, the value of the expression 5 / 9 = 0 is also calculated correctly. So by the precedence of the operators, the value of the expression 5 / 9 * (fahrenheit - 32) will always be 0 regardless of the value of fahrenheit. So the problem is in the integer division. We can replace the expression 5 / 9 with 5.0 / 9. In this case, the value of the expression 5.0 / 9 * (fahrenheit - 32) will be a decimal number. Because fahrenheit and celsius are `int` variables, we can use the cast operators to convert this value to an integer, that is, we use the following expression:

```cpp
celsius = static_cast<int> (5.0 / 9 * (fahrenheit - 32) + 0.5);
```

(Note that in the preceding expression, we added 0.5 to round the number to the nearest integer.)

The revised program is:

```cpp
#include <iostream>                              //Line 1

using namespace std;                              //Line 2

int main()                                        //Line 3
{
    int fahrenheit;                               //Line 4
    int celsius;                                   //Line 5
                                                    //Line 6

    cout << "Enter temperature in Fahrenheit: ";        //Line 7
    cin >> fahrenheit;                                  //Line 8
    cout << endl;                                        //Line 9

    celsius = static_cast<int>
        (5.0 / 9 * (fahrenheit - 32) + 0.5);             //Line 10

    cout << fahrenheit << " degree F = "
         << celsius << " degree C." << endl;             //Line 11

    return 0;                                             //Line 12
}                                                     //Line 13
```

**Sample Run:** In this sample run, the user input is shaded.

Enter temperature in Fahrenheit: `110`

110 degree F = 43 degree C.

As we can see, using temporary cout statements, we were able to find the problem. After correcting the problem, the temporary cout statements are removed.

The temperature conversion program contained logic errors, not syntax errors. Using cout statements to print the values of expressions and/or variables to see the results of a calculation is an effective way to find and correct logic errors.

## File Input/Output

The previous sections discussed in some detail how to get input from the keyboard (standard input device) and send output to the screen (standard output device). However, getting input from the keyboard and sending output to the screen have several limitations. Inputting data in a program from the keyboard is comfortable as long as the amount of input is very small. Sending output to the screen works well if the amount of data is small (no larger than the size of the screen) and you do not want to distribute the output in a printed format to others.

If the amount of input data is large, however, it is inefficient to type it at the keyboard each time you run a program. In addition to the inconvenience of typing large amounts of data, typing can generate errors, and unintentional typos cause erroneous results. You must have some way to get data into the program from other sources. By using alternative sources of data, you can prepare the data before running a program, and the program can access the data each time it runs.

Suppose you want to present the output of a program in a meeting. Distributing printed copies of the program output is a better approach than showing the output on a screen. For example, you might give a printed report to each member of a committee before an important meeting. Furthermore, output must sometimes be saved so that the output produced by one program can be used as an input to other programs.

This section discusses how to obtain data from other input devices, such as a disk (that is, secondary storage), and how to save the output to a disk. C++ allows a program to get data directly from and save output directly to secondary storage. A program can use the file I/O and read data from or write data to a file. Formally, a file is defined as follows:

**File:** An area in secondary storage used to hold information.

The standard I/O header file, `iostream`, contains data types and variables that are used only for input from the standard input device and output to the standard output device. In addition, C++ provides a header file called `fstream`, which is used for file I/O. Among other things, the `fstream` header file contains the definitions of two data types: `ifstream`, which means input file stream and is similar to `istream`, and `ofstream`, which means output file stream and is similar to `ostream`.

The variables `cin` and `cout` are already defined and associated with the standard input/output devices. In addition, `>>`, `get`, `ignore`, `putback`, `peek`, and so on can be used with `cin`, whereas `<<`, `setfill`, and so on can be used with `cout`. These same operators and functions are also available for file I/O, but the header file `fstream` does not declare variables to use them. You must declare variables called **file stream variables**, which include `ifstream` variables for input and `ofstream` variables for output. You then use these variables together with `>>`, `<<`, or other functions for I/O. Remember that C++ does not automatically initialize user-defined variables. Once you declare the `fstream` variables, you must associate these file variables with the input/output sources.

File I/O is a five-step process:

- 1. Include the header file `fstream` in the program.
- 2. Declare file stream variables.
- 3. Associate the file stream variables with the input/output sources.
- 4. Use the file stream variables with `>>`, `<<`, or other input/output functions.
- 5. Close the files.

We will now describe these five steps in detail. A skeleton program then shows how the steps might appear in a program.

Step 1 requires that the header file `fstream` be included in the program. The following statement accomplishes this task:

```cpp
#include <fstream>
```

Step 2 requires you to declare file stream variables. Consider the following statements:

```cpp
ifstream inData;
ofstream outData;
```

The first statement declares `inData` to be an input file stream variable. The second statement declares `outData` to be an output file stream variable.

Step 3 requires you to associate file stream variables with the input/output sources. This step is called **opening the files**. The stream member function `open` is used to open files. The syntax for opening a file is:

```cpp
fileStreamVariable.open(sourceName);
```
