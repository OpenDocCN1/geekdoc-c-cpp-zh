# Specifying the Type for Enumeration Constants

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

# Basic Input/Output Operations

Here, you will only look at enough of native C++ input and output to get you through learning about C++. It’s not that it’s difficult — quite the opposite in fact — but for Windows programming you won’t need it at all. C++ input/output revolves around the notion of a data stream, where you can insert data into an output stream or extract data from an input stream. You have already seen that the ISO/ANSI C++ standard output stream to the command line on the screen is referred to as cout. The complementary input stream from the keyboard is referred to as cin.

# Input from the Keyboard

You obtain input from the keyboard through the stream cin, using the extractor operator for a stream >>. To read two integer values from the keyboard into integer variables num1 and num2, you can write this statement:

```
cin >> num1 >> num2;
```

The extraction operator, >>, “points” in the direction that data flows — in this case, from cin to each of the two variables in turn. Any leading whitespace is skipped, and the first integer value you key in is read into num1. This is because the input statement executes from left to right. Any whitespace following