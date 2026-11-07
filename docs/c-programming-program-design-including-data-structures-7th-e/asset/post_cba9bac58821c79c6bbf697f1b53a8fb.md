
only when they are activated—that is, called. C++ comes with a wealth of functions, called **predefined functions**, that are already written. In this section, you will learn how to use some predefined functions that are provided as part of the C++ system. Later in this chapter, you will learn how to use stream functions to perform a specific I/O operation.

Recall from Chapter 2 that predefined functions are organized as a collection of libraries, called header files. A particular header file may contain several functions. Therefore, to use a particular function, you need to know the name of the function and a few other things, which are described shortly.

A very useful function, `pow`, called the power function, can be used to calculate x^y in a program. That is, `pow(x, y) = x^y`. For example, `pow(2.0, 3.0) = 2.0^3 = 8.0` and `pow(4.0, 0.5) = 4.0^0.5 = 2.0`. The numbers x and y that you use in the function `pow` are called the **arguments** or **parameters** of the function `pow`. For example, in `pow(2.0, 3.0)`, the parameters are 2.0 and 3.0.

An expression such as `pow(2.0, 3.0)` is called a **function call**, which causes the code attached to the predefined function `pow` to execute and, in this case, computes 2.0^3.0. The header file `cmath` contains the specification of the function `pow`.

To use a predefined function in a program, you need to know the name of the header file containing the specification of the function and include that header file in the program. In addition, you need to know the name of the function, the number of parameters the function takes, and the type of each parameter. You must also be aware of what the function is going to do. For example, to use the function `pow`, you must include the header file `cmath`. The function `pow` has two parameters, which are decimal numbers. The function calculates the first parameter to the power of the second parameter. (Appendix F describes some commonly used header files and predefined functions.)

The program in the following example illustrates how to use predefined functions in a program. More specifically, we use some math functions, from the header file `cmath`, and the string function `length`, from the header file `string`. Note that the function `length` determines the length of a string.

### EXAMPLE 3-4

```cpp
//How to use predefined functions.
//This program uses the math functions pow and sqrt to determine
//and output the volume of a sphere, the distance between two
//points, respectively, and the string function length to find
//the number of characters in a string.
//If the radius of the sphere is r, then the volume of the sphere
//is (4/3)*PI*r^3. If (x1,y1) and (x2,y2) are the coordinates of two
//points in the x-y plane, then the distance between these points is
//sqrt((x1-x2)^2 + (y2-y1)^2)

#include <iostream>
#include <cmath>
#include <string>

using namespace std;

const double PI = 3.1416;

int main()
{
        double sphereRadius;                                      //Line 1
        double sphereVolume;                                      //Line 2
        double point1X, point1Y;                                  //Line 3
        double point2X, point2Y;                                  //Line 4
        double distance;                                          //Line 5

        string str;                                               //Line 6

        cout << "Line 7: Enter the radius of the sphere: ";      //Line 7
        cin >> sphereRadius;                                      //Line 8
        cout << endl;                                             //Line 9

        sphereVolume = (4.0 / 3) * PI * pow(sphereRadius, 3);     //Line 10

        cout << "Line 11: The volume of the sphere is: "
             << sphereVolume << endl << endl;                     //Line 11

        cout << "Line 12: Enter the coordinates of two "
             << "points in the X-Y plane: ";                      //Line 12
        cin >> point1X >> point1Y >> point2X >> point2Y;          //Line 13
        cout << endl;                                             //Line 14

        distance = sqrt(pow(point2X - point1X, 2)
                      + pow(point2Y - point1Y, 2));               //Line 15

        cout << "Line 16: The distance between the points "
             << "(" << point1X << ", " << point1Y << ") and "
             << "(" << point2X << ", " << point2Y << ") is: "
             << distance << endl << endl;                         //Line 16

        str = "Programming with C++";                             //Line 17

        cout << "Line 18: The number of characters, "
             << "including blanks, in \"" << str << "\" is:"
             << str.length() << endl;                             //Line 18

        return 0;                                                 //Line 19
}
```

**Sample Run:** In this sample run, the user input is shaded.

```
Line 7: Enter the radius of the sphere: 3

Line 11: The volume of the sphere is: 113.098

Line 12: Enter the coordinates of two points in the X-Y plane: 4 7 9 -5

Line 16: The distance between the points (4, 7) and (9, -5) is: 13

Line 18: The number of characters, including blanks, in "Programming with C++" is: 20
```

The preceding program works as follows. The statements in Lines 1 to 6 declare the variables used in the program. The statement in Line 7 prompts the user to enter the radius of the sphere, and the statement in Line 8 stores the radius in the variable `sphereRadius`. The statement in Line 10 uses the function `pow` to compute and store the volume of the sphere in the variable `sphereVolume`. The statement in Line 11 outputs the volume. The statement in Line 12 prompts the user to enter the coordinates of two points in the X-Y plane, and the statement in Line 13 stores the coordinates in the variables `point1X`, `point1Y`, `point2X`, and `point2Y`, respectively. The statement in Line 15 uses the functions `sqrt` and `pow` to determine the distance between the points. The statement in Line 16 outputs the distance between the points. The statement in Line 17 stores the string "Programming with C++" in `str`. The statement in Line 18 uses the string function `length` to determine and output the length of `str`. Note how the function `length` is used. Later in this chapter we will explain the meaning of expressions such as `str.length()`.

Because I/O is fundamental to any programming language and because writing instructions to perform a specific I/O operation is not a job for everyone, every programming language provides a set of useful functions to perform specific I/O operations. In the remainder of this chapter, you will learn how to use some of these functions in a program. As a programmer, you must pay close attention to how these functions are used so that you can get the most out of them. The first function you will learn about here is the function `get`.

### cin and the get Function

As you have seen, the extraction operator skips all leading whitespace characters when scanning for the next input value. Consider the variable declarations:

```
    char ch1, ch2;
    int num;
```

and the input:

```
A 25
```

Now consider the following statement:

```
    cin >> ch1 >> ch2 >> num;
```

When the computer executes this statement, 'A' is stored in `ch1`, the blank is skipped by the extraction operator `>>`, the character '2' is stored in `ch2`, and 5 is stored in `num`. However, what if you intended to store 'A' in `ch1`, the blank in `ch2`, and 25 in `num`? Is it clear that you cannot use the extraction operator `>>` to input this data.

As stated earlier, sometimes you need to process the entire input, including whitespace characters, such as blanks and the newline character. For example, suppose you want to process the entered data on a line-by-line basis. Because the extraction operator `>>` skips the newline character and unless the program captures the newline character, the computer does not know where one line ends and the next begins.

The variable `cin` can access the stream function `get`, which is used to read character data. The `get` function inputs the very next character, including whitespace characters, from the input stream and stores it in the memory location indicated by its argument. The function `get` comes in many forms. Next, we discuss the one that is used to read a character.

The syntax of `cin`, together with the `get` function to read a character, follows:

```
    cin.get(varChar);
```

In the `cin.get` statement, `varChar` is a char variable. `varChar`, which appears in parentheses following the function name, is called the argument or parameter of the function. The effect of the preceding statement would be to store the next input character in the variable `varChar`.

Now consider the following input again:

```
A 25
```

To store 'A' in `ch1`, the blank in `ch2`, and 25 in `num`, you can effectively use the `get` function as follows:

```
    cin.get(ch1);
    cin.get(ch2);
    cin >> num;
```

Because this form of the `get` function has only one argument and reads only one character and you need to read two characters from the input stream, you need to call this function twice. Notice that you cannot use the `get` function to read data into the variable `num` because `num` is an int variable. The preceding form of the `get` function reads values of only the char data type.

The preceding set of `cin.get` statements is equivalent to the following statements:

```
    cin >> ch1;
    cin.get(ch2);
    cin >> num;
```

> The function `get` has other forms, one of which you will study in Chapter 8. For the next few chapters, you need only the form of the function `get` introduced here.
