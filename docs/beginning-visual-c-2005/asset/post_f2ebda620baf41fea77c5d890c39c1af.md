
## Chapter 2: Data, Variables, and Calculations

![Figure 2-13](img/2359b0c604600c58fba3539c738a356e_143_0.png)

Figure 2-13

When you click on the OK button, the Application Wizard will generate the project containing the following code:

```
// Ex2_12.cpp : main project file.

#include "stdafx.h"

using namespace System;

int main(array<System::String ^> ^args)
{
    Console::WriteLine(L"Hello World");
    return 0;
}
```

I’m sure you’ve noticed the extra stuff between the parentheses following main. This is concerned with passing values to the function main() when you initiate execution of the program from the command line, and you’ll learn more about this when you explore functions in detail. If you compile and execute the default project, it will write "Hello World" to the command line. Now, you’ll convert this program to a CLR version of Ex2_02 so you can see how similar it is. To do this, you can modify the code in Ex2_12.cpp as follows:

```
// Ex2_12.cpp : main project file.
#include "stdafx.h"

using namespace System;

int main(array<System::String ^> ^args)
{
    int apples, oranges; // Declare two integer variables
    int fruit; // ...then another one
    apples = 5; oranges = 6; // Set initial values
    fruit = apples + oranges; // Get the total fruit
    Console::WriteLine(L"\nOranges are not the only fruit...");
    Console::Write(L"- and we have ");
    Console::Write(fruit);
    Console::Write(L" fruits in all.\n");
    return 0;
}
```

The new lines are shown shaded, and those in the lower block replace the two lines in the automatically generated version of main(). You can now compile and execute the project. The program should produce the following output:

```
Oranges are not the only fruit...
- and we have 11 fruits in all.
```

The only significant difference is in how the output is produced. The definitions for the variables and the computation are the same. Although you are using the same type names as in the ISO/ANSI C++ version of the example, the effect is not the same. The variables apples, oranges, and fruit will be of the C++/CLI type int, that is specified by type int, and they have some additional capabilities compared to the ISO/ANSI type. The variables here can act as objects in some circumstances or as simple values as they do here. If you want to confirm that Int32 is the same as int in this case, you could replace the int type name with Int32 and recompile the example. It should work in exactly the same way.

```
Console::WriteLine(L"\nOranges are not the only fruit...");
```

The WriteLine() function is a C++/CLI function that is defined in the Console class in the System namespace. You’ll learn about classes in detail in Chapter 6, but for now the Console class represents the standard input and output streams that correspond to the keyboard and the command line in a command line window. Thus the WriteLine() function writes whatever is between the parentheses following the function name to the command line and then writes a newline character to move the cursor to the next line ready for the next output operation. Thus the preceding statement writes the text "Oranges are not the only fruit..." between the double quotes to the command line. The L preceding the string indicates that it is a wide-character string where each character occupies two bytes.

The Write() function in the Console class is essentially the same as the WriteLine() function, the only difference being that it does not automatically write a newline character following the output that you specify. You can therefore use the Write() function when you want to write two or more items of data to the same line in individual output statements.

```
referenced by:          0    1    2    etc.
Console::WriteLine("Format string", arg2, arg3, arg4,... );
```

Thus the zero between the braces in the previous code fragment indicates that the value of the packageCount argument should replace the {0} in the string that is to be written to the command line.

If you want to output the weight as well as the number of packages, you could write this:

```
int packageCount = 25;
double packageWeight = 7.5;
Console::WriteLine(L"There are {0} packages weighing {1} pounds.",
                    packageCount,
                    packageWeight);
```

The output statement now has three arguments, and the second and third arguments are referenced by 0 and 1, respectively, between the braces. So, this will produce the output:

```
There are 25 packages weighing 7.5 pounds.
```

You could also write the statement with the last two arguments in reverse sequence, like this:

```
Console::WriteLine(L"There are {1} packages weighing {0} pounds.",
                    packageWeight,
                    packageCount);
```

The packageWeight variable is now referenced by 0 and packageCount by 1 in the format string, and the output will be the same as previously.

You also have the possibility to specify how the data is to be presented on the command line. Suppose that you wanted the floating-point value packageWeight to be output with two places of decimals. You could do that with the following statement:

```
Console::WriteLine(L"There are {0} packages weighing {1:F2} pounds.",
                    packageCount, packageWeight);
```

In the substring {1:F2}, the colon separates the index value, 1, that identifies the argument to be selected from the format specification that follows, F2. The F in the format specification indicates that the output should be in the form "ddd.dd..." (where d represents a digit) and the 2 indicates that you want to have two decimal places after the point. The output produced by the statement will be:

```
There are 25 packages weighing 7.50 pounds.
```

In general, you can write the format specification in the form {n,w:Axx} where n is an index value selecting the argument following the format string, w is an optional field width specification, A is a single letter specifying how the value should be formatted, and xx is an optional one or two digits specifying the precision for the value. The field width specification is a signed integer. The value will be right-justified in the field if w is positive and left-justified when it is negative. If the value occupies less than the number of positions specified by w the output is padded with spaces; if the value requires more positions than that specified by w the width specification is ignored. Here’s another example:

```
Console::WriteLine(L"Packages:{0,3} Weight: {1,5:F2} pounds.",
                    packageCount, packageWeight);
```

The package count is output with a field width of 3 and the weight in a field width of 5, so the output will be:

```
Packages: 25 Weight:  7.50 pounds.
```

There are other format specifiers that enable you to present various types of data in different ways. Here are some of the most useful format specifications:

| Format Specifier | Description |
|---|---|
| C or c | Outputs the value as a currency amount. |
| D or d | Outputs an integer as a decimal value. If you specify the precision to be more than the number of digits, the number will be padded with zeroes to the left. |
| E or e | Outputs a floating-point value in scientific notation, that is, with an exponent. The precision value will indicate the number of digits to be output following the decimal point. |
| F or f | Outputs a floating-point value as a fixed-point number of the form ±dddd.dd.... |
| G or g | Outputs the value in the most compact form depending on the type of the value and whether you have specified the precision. If you don’t specify the precision, a default precision value will be used. |
| N or n | Outputs the value as a fixed-point decimal value using comma separators between each group of three digits when necessary. |
| X or x | Outputs an integer as a hexadecimal value. Upper or lowercase hexadecimal digits will be output depending on whether you specify X or x. |

That gives you enough of a toehold in output to continue with more C++/CLI examples. Now you’ll take a quick look at some of this in action.

### Try It Out: Formatted Output

Here’s an example that calculates the price of a carpet to demonstrate output in a CLR console program:

```
// Ex2_13.cpp : main project file.
// Calculating the price of a carpet
#include "stdafx.h"

using namespace System;

int main(array<System::String ^> ^args)
{
    double carpetPriceSqYd = 27.95;
    double roomWidth = 13.5;            // In feet
    double roomLength = 24.75;          // In feet
    const int feetPerYard = 3;
```
