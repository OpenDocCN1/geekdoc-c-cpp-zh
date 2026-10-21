
## Defining Synonyms for Data Types

The typedef keyword enables you to define your own type name for an existing type. Using typedef, you could define the type name BigOnes as equivalent to the standard long int type with the declaration:

```
typedef long int BigOnes;      // Defining BigOnes as a type name
```

This defines BigOnes as an alternative type specifier for long int, so you could declare a variable mynum as long int with the declaration:

```
BigOnes mynum = 0L;           // Define a long int variable
```

There’s no difference between this declaration and the one using the built-in type name. You could equally well use:

```
long int mynum = 0L;          // Define a long int variable
```

for exactly the same result. In fact, if you define your own type name such as BigOnes, you can use both type specifiers within the same program for declaring different variables that will end up as having the same type.

Since typedef only defines a synonym for an existing type, it may appear to be a bit superficial, but it is not at all. You’ll see later that it fulfills a very useful role in enabling you to simplify more complex declarations by defining a single name that represents a somewhat convoluted type specification, and this can make your code much more readable.

## Variables with Specific Sets of Values

You will sometimes be faced with the need for variables that have a limited set of possible values that can be usefully referred to by labels — the days of the week, for example, or months of the year. There is a specific facility in C++ to handle this situation, called an enumeration. Take one of the examples I have just mentioned — a variable that can assume values corresponding to days of the week. You can define this as follows:

```
enum Week{Mon, Tues, Wed, Thurs, Fri, Sat, Sun} thisWeek;
```

This declares an enumeration type with the name Week and the variable thisWeek, which is an instance of the enumeration type Week that can assume only the constant values specified between the braces. If you try to assign to thisWeek anything other than one of the set of values specified, it will cause an error. The symbolic names listed between the braces are known as enumerators. In fact, each of the names of the days will be automatically defined as representing a fixed integer value. The first name in the list, Mon, will have the value 0, Tues will be 1, and so on.

You could assign one of the enumeration constants as the value of the variable thisWeek like this:

```
thisWeek = Thurs;
```

## Data, Variables, and Calculations

Note that you do not need to qualify the enumeration constant with the name of the enumeration. The value of thisWeek will be 3 because the symbolic constants that an enumeration defines are assigned values of type int by default in sequence starting with 0.

By default, each successive enumerator is one larger than the value of the previous one, but if you would prefer the implicit numbering to start at a different value, you can just write:

```
enum Week {Mon = 1, Tues, Wed, Thurs, Fri, Sat, Sun} thisWeek;
```

Now the enumeration constants will be equivalent to 1 through 7. The enumerators don’t even need to have unique values. You could define Mon and Tues as both having the value 1, for example, with the statement:

```
enum Week {Mon = 1, Tues = 1, Wed, Thurs, Fri, Sat, Sun} thisWeek;
```

As the type of the variable thisWeek is type int, it will occupy four bytes, as will all variables that are of an enumeration type.

Having defined the form of an enumeration, you can define another variable thus:

```
enum Week nextWeek;
```

This defines a variable nextWeek as an enumeration that can assume the values previously specified. You can also omit the enum keyword in declaring a variable, so, instead of the previous statement, you could write:

```
Week next_week;
```

If you wish, you can assign specific values to all the enumerators. For example, you could define this enumeration:

```
enum Punctuation {Comma = ',', Exclamation = '!', Question = '?'} things;
```

Here you have defined the possible values for the variable things as the numerical equivalents of the appropriate symbols. If you look in the ASCII table in Appendix B, you will see that the symbols are 44, 33 and 63, respectively, in decimal. As you can see, the values assigned don’t have to be in ascending order. If you don’t specify all the values explicitly, each enumerator will be assigned a value incrementing by 1 from the last specified value, as in our second Week example.

You can omit the enumeration type if you don’t need to define other variables of this type later. For example:

```
enum {Mon, Tues, Wed, Thurs, Fri, Sat, Sun} thisWeek, nextWeek, lastWeek;
```

Here you have three variables declared that can assume values from Mon to Sun. Because the enumeration type is not specified, you cannot refer to it. Note that you cannot define other variables for this enumeration at all, because you would not be permitted to repeat the definition. Doing so would imply that you were redefining values for Mon to Sun, and this isn’t allowed.

## Specifying the Type for Enumeration Constants

Enumeration constants are type int by default, but you can also choose to specify the type explicitly by adding a colon and the type name for the constants following the enumeration type name in the declaration. You can specify the type for the enumeration constants as any of the signed or unsigned integer types: short, int, long, and char, or as type bool.

Thus, you could define the enumeration representing days of the week as:

```
enum Week: char{ Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday };
```

Here the enumeration constants will be of type char with the first constant as 0. However, with the constants as type char you might prefer to initialize them explicitly, like this:

```
enum Week : char{ Monday='M', Tuesday='T', Wednesday='W',
    Thursday='T', Friday='F', Saturday='S', Sunday='S'};
```

Now the values for the constants reflect a little more what they represent, although they do not distinguish between Thursday and Tuesday or between Saturday and Sunday. There is no problem with having duplicate values for the constants, but of course, all the names must be unique.

Here’s an example of an enumeration with bool constants:

```
enum State : bool { On = true, Off };
```

Because On has the initial value true, Off will be false. If there were subsequent enumerations constants specified, they would alternate in value by default.

## Basic Input/Output Operations

Here, you will only look at enough of native C++ input and output to get you through learning about C++. It’s not that it’s difficult — quite the opposite in fact — but for Windows programming you won’t need it at all. C++ input/output revolves around the notion of a data stream, where you can insert data into an output stream or extract data from an input stream. You have already seen that the ISO/ANSI C++ standard output stream to the command line on the screen is referred to as cout. The complementary input stream from the keyboard is referred to as cin.

## Input from the Keyboard

You obtain input from the keyboard through the stream cin, using the extractor operator for a stream >>. To read two integer values from the keyboard into integer variables num1 and num2, you can write this statement:

```
cin >> num1 >> num2;
```

The extraction operator, >>, “points” in the direction that data flows — in this case, from cin to each of the two variables in turn. Any leading whitespace is skipped, and the first integer value you key in is read into num1. This is because the input statement executes from left to right. Any whitespace following

line. Because output statements execute from left to right, the second output statement displays the value of num1 followed by the value of num2.

When you compile and execute this, you will get the output:

```
12345678
```

The output is correct, but it’s not exactly helpful. You really need the two output values to be separated by at least one space. The default for stream output is to just output the digits in the output value, which doesn’t provide for spacing successive output values out nicely so they can be differentiated. As it is, you have no way to tell where the first number ends and the second number begins.

## Formatting the Output

You can fix the problem of there being no spaces between items of data quite easily, though, just by outputting a space between the two values. You can do this by replacing the following line in your original program:

```
cout << num1 << num2;            // Output two values
```

Just substitute the statement:

```
cout << num1 << ' ' << num2;            // Output two values
```

Of course, if you had several rows of output that you wanted to align in columns, you would need some extra capability because you do not know how many digits there will be in each value. You can take care of this situation by using what is called a manipulator. A manipulator modifies the way in which data output to (or input from) a stream is handled.

Manipulators are defined in the header file <iomanip>, so you need to add an #include directive for it. The manipulator that you’ll use is setw(n), which will output the value that follows right-justified in a field n spaces wide, so setw(6) causes the next output value to be presented in a field with a width of six spaces. Let’s see it working.

## Try It Out    Using Manipulators

To get something more like the output you want, you can change the program to the following:

```
// Ex2_03.cpp
// Exercising output
#include <iostream>
#include <iomanip>

using std::cout;
using std::endl;
using std::setw;

int main()
{
    int num1 = 1234, num2 = 5678;
