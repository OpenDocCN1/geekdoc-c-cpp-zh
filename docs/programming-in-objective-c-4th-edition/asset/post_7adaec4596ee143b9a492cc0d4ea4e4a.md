
# 4. Data Types and Expressions

In this chapter, we take a look at the basic data types and describe some fundamental rules for forming arithmetic expressions in Objective-C.

## Data Types and Constants

You have already encountered the Objective-C basic data type int. As you will recall, a variable declared to be of type int can be used to contain integral values only—that is, values that do not contain decimal digits.

The Objective-C programming language provides three other basic data types: float, double, and char. A variable declared to be of type float can be used for storing floating-point numbers (containing decimal digits). The double type is the same as type float, typically with roughly twice the range. Finally, the char data type can be used to store a single character, such as the letter a, the digit character 6, or a semicolon (more on this later).

In Objective-C, any literal number, single character, or character string is known as a constant. For example, the number 58 represents a constant integer value. The string @"Programming in Objective-C is fun." is an example of a constant string object. Expressions consisting entirely of constant values are called constant expressions. So this expression is a constant expression because each of the terms of the expression is a constant value:

```
128 + 7 - 17
```

But if i were declared to be an integer variable, this expression would not represent a constant expression:

```
128 + 7 - i
```

## Type int

An integer consists of the sequence of one or more digits. A minus sign preceding the sequence indicates that the value is negative. The values 158, -10, and 0 are all valid examples of integer constants. No embedded spaces are permitted between the digits, and commas can't be used.(So the value 12,000 is not a valid integer constant and must be written as 12000.)

Every value, whether it's a character, an integer, or a floating-point number, has a range of values associated with it. This range has to do with the amount of storage allocated to store a particular type of data. In general, that amount is not defined in the language; it typically depends on the computer you're running on and is therefore called implementation or machine dependent. For example, an integer variable might take 32 bits on your computer, or perhaps it might be stored in 64. If 64 bits were used, then much larger numbers can be stored inside integer variables than if 32 bits were used instead.

> Note

> Under Mac OS X, you are given the option of compiling an application as either a 32-bit or 64-bit application. In the former case, an int takes up 32 bits; in the latter case, 64 bits are used.

## Type float

You can use a variable declared to be type float to store values containing decimal digits. A floating-point constant is distinguished by the presence of a decimal point. The values 3., 125.8, and -.0001 are all valid examples of floating-point constants. To display a floating-point value, the NSLog conversion characters %f or %g can be used.

Floating-point constants can also be expressed in so-called scientific notation. The value 1.7e4 is a floating-point value expressed in this notation that represents the value 1.7 x 10⁴.

As noted, the double type is the same as type float, with only twice the range.

## Type char

You can use a char variable to store a single character. A character constant is formed by enclosing the character within a pair of single quotation marks. So 'a', ';', and '0' are all valid examples of character constants. The first constant represents the letter a, the second is a semicolon, and the third is the character zero—which is not the same as the number. Do not confuse a character constant, which is a single character enclosed in single quotes, with a C-style character string, which is any number of characters enclosed in double quotes. As mentioned in the last chapter, a string of characters enclosed in a pair of double quotes that is preceded by an @ character is an NSString character object.

The character '\n', the newline character, is a valid character even though it seems to contradict the rule cited previously. The reason for this is that the backslash character is recognized as a special character. In other words, the Objective-C compiler treats the character '\n' as a single character, even though it is actually formed by two characters. Other special characters are initiated with the backslash character. The format characters %c can be used in an NSLog call to display the value of a char variable.

Program 4.1 uses the basic Objective-C data types.

## Program 4.1

```
#import <Foundation/Foundation.h>

int main (int argc, char * argv[]) {
    @autoreleasepool {
        int integerVar = 100;
        float floatingVar = 331.79;
        double doubleVar = 8.44e+11;
        char charVar = 'W';

        NSLog("@integerVar = %i", integerVar);
        NSLog("@floatingVar = %f", floatingVar);
        NSLog("@doubleVar = %e", doubleVar);
        NSLog("@doubleVar = %g", doubleVar);
        NSLog("@charVar = %c", charVar);
    }
    return 0;
}
```

## Program 4.1. Output

```
integerVar = 100
floatingVar = 331.790000
doubleVar = 8.44e+11
doubleVar = 8.44e+11
charVar = W
```
