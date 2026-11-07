
column position when the subsequent statements output the values of the variables. The statement in Line 4 outputs the value of `x` in five columns, the value of `y` in seven columns, and the string `"Warm"` in eight columns. In this statement, the filling character is the blank character, as shown in the second line of output.

The statement in Line 5 sets the filling character to `*`. The statement in Line 6 outputs the value of `x` in five columns, the value of `y` in seven columns, and the string `"Warm"` in eight columns. Because `x` is a two-digit number and five columns are assigned to output its value, the first three columns are unused by `x` and are, therefore, filled by the filling character `*`. To print the value of `y`, seven columns are assigned; `y` is a four-digit number, however, so the filling character fills the first three columns. Similarly, to print the value of the string `"Warm"`, eight columns are assigned; the string `"Warm"` has only four characters, so the filling character fills the first four columns. See the third line of output.

The output of the statement in Line 7—the fourth line of output—is similar to the output of the statement in Line 6, except that the filling character for `y` and the string `"Warm"` is `#`. In the output of the statement in Line 8 (the fifth line of output), the filling character for `x` is `0`, the filling character for `y` is `#`, and the filling character for the string `"Warm"` is `^`. The manipulator `setfill` sets these filling characters.

The statement in Line 9 sets the filling character to blank. The statement in Line 10 outputs the values of `x`, `y`, and the string `"Warm"` using the filling character blank, as shown in the sixth line of output.

## Left and Right Manipulators

Recall that if the number of columns specified in the `setw` manipulator exceeds the number of columns required by the next expression, the default output is right-justified. Sometimes, you might want the output to be left-justified. To left-justify the output, you use the manipulator `left`.

The syntax to set the manipulator `left` is:

```cpp
ostreamVar << left;
```

where `ostreamVar` is an output stream variable. For example, the following statement sets the output to be left-justified on the standard output device:

```cpp
cout << left;
```

You can disable the manipulator `left` by using the stream function `unsetf`. The syntax to disable the manipulator `left` is:

```cpp
ostreamVar.unsetf(ios::left);
```

where `ostreamVar` is an output stream variable. Disabling the manipulator `left` returns the output to the settings of the default output format. For example, the following statement disables the manipulator `left` on the standard output device:

```cpp
cout.unsetf(ios::left);
```

The syntax to set the manipulator `right` is:

```cpp
ostreamVar << right;
```

where `ostreamVar` is an output stream variable. For example, the following statement sets the output to be right-justified on the standard output device:

```cpp
cout << right;
```

> **NOTE** On some compilers, the statements `cin >> left;` and `cin >> right;` might not work. In this case, you can use `cin.setf(ios::left);` in place of `cin >> left;` and `cin.setf(ios::right);` in place of `cin >> right;`.

The program in Example 3–14 illustrates the effect of the manipulators `left` and `right`.

### Example 3-14

```cpp
//Example: left justification

#include <iostream>
#include <iomanip>

using namespace std;

int main()
{
    int x = 15;                                      //Line 1
    int y = 7634;                                    //Line 2

    cout << left;                                    //Line 3

    cout << "12345678901234567890" << endl;         //Line 4
    cout << setw(5) << x << setw(7) << y
         << setw(8) << "Warm" << endl;              //Line 5

    cout << setfill('*');                            //Line 6

    cout << setw(5) << x << setw(7) << y
         << setw(8) << "Warm" << endl;              //Line 7

    cout << setw(5) << x << setw(7) << setfill('#')
         << y << setw(8) << "Warm" << endl;         //Line 8

    cout << setw(5) << setfill('@') << x
         << setw(7) << setfill('#') << y
         << setw(8) << setfill('^') << "Warm"        //Line 9
         << endl;

    cout << right;                                //Line 10
    cout << setfill(' ');                         //Line 11

    cout << setw(5) << x << setw(7) << y          //Line 12
         << setw(5) << "Warm" << endl;

    return 0;
}
```

### Sample Run:

```text
12345678901234567890
15    7634    Warm
15***7634***Warm****
15***7634###Warm####
15@@@7634###Warm^^^^
    15  7634    Warm
```

The output of this program is the same as the output of Example 3-11. The only difference here is that for the statements in Lines 4 through 9, the output is left-justified. You are encouraged to do a walk-through of this program.

> **NOTE**
>
> This chapter discusses several stream functions and stream manipulators. To use stream functions such as `get`, `ignore`, `fill`, and `clear` in a program, the program must include the header file `iostream`.
>
> There are two types of manipulators: those with parameters and those without parameters. Manipulators with parameters are called **parameterized stream manipulators**. For example, manipulators such as `setprecision`, `setw`, and `setfill` are parameterized. On the other hand, manipulators such as `endl`, `fixed`, `scientific`, `showpoint`, and `left` do not have parameters.
>
> To use a parameterized stream manipulator in a program, you must include the header file `iomanip`. Manipulators without parameters are part of the `iostream` header file and, therefore, do not require inclusion of the header file `iomanip`.

## Input/Output and the `string` Type

You can use an input stream variable, such as `cin`, and the extraction operator `>>` to read a string into a variable of the data type `string`. For example, if the input is the string "Shelly", the following code stores this input into the `string` variable `name`:

```cpp
string name;    //variable declaration
cin >> name;    //input statement
```

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
myString    "Hello there. How are you?"
```

All 29 characters, including the first four blanks, are stored into myString.

Similarly, you can use an output stream variable, such as cout, and the insertion operator << to output the contents of a variable of the data type string.

## Debugging: Understanding Logic Errors and Debugging with cout Statements

In the debugging section of Chapter 2, we illustrated how to understand and correct syntax errors. As we have seen, syntax errors are reported by the compiler, and the compiler not only reports syntax errors, but also gives some explanation about the errors. On the other hand, logic errors are typically not caught by the compiler except for the trivial ones such as using a variable without properly initializing it. In this section, we illustrate how to spot and

![](img/f97f778697507bb6fdd80c5991210cba_190_0.png)
