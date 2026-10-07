# Chapter 6 Making Decisions

This clause determines whether the character is a digit. Note that this test compares the character c against the characters '0' and '9' and not the integers 0 and 9. This is because a character was read from the terminal, and the characters '0' to '9' are not the same as the numbers 0-9. In fact, in ASCII, the character '0' is actually represented as the number 48, the character '1' as the number 49, and so on.

If c is a digit, the phrase "It's a digit." is displayed. Otherwise, if c is not alphabetic and not a digit, the final else clause is executed and displays the phrase "It's a special character" at the terminal. Execution of the program is then complete.

Even when used to read just a single character, you must still press the Return key after the character to send it to the program. In general, whenever you're reading data from the terminal, the program doesn't see any of the data type used until the line the Return key is pressed.

Let's suppose for the next example that you want to write a program that allows the user to type in simple expressions of the following:

+   number operator number

The program will evaluate and display the results at the terminal. The operators you want to have recognized the normal operators for addition, subtraction, multiplication, and division. Let's use the Calculator class from Program 4.6 in Chapter 4,"Data Types and Expressions," here. Each expression will be given to the calculator for computation.

The following program uses a large statement with many if clauses to determine which operation is to be performed.

> Note
It's better to use routines in the standard library called islower and isupper, and avoid the internal representation issue entirely. To do that, include the #import <ctype.h> in your program. However, we put this phrase here for illustrative purposes only.

# Program 6.8

```
// Program to evaluate simple expressions of the form
// number operator number

// Implement a Calculator class
#import <Foundation/Foundation.h>

@interface NSObject
{
  double accumulator;
}

// accumulator methods
-(void) setAccumulator:(double) value;
-(void) clear;
-(double) accumulator;
```