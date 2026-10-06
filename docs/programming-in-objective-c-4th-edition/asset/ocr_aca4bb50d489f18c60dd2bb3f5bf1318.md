find the value of the 200th triangular number, for example? It certainly would be tedious to have modify Program 5.1 to explicitly add up all the integers from 1 to 200. Luckily, there is an easier way.

One of the fundamental properties of a computer is its capability to repeatedly execute a set of statements. These looping capabilities enable programmers to develop concise programs containing repetitive processes that could otherwise require thousands or even millions of program statements to perform. The Objective-C language contains three program statements for program looping.

# The for Statement

Let's take a look at a program that uses the for statement. The purpose of Program 5.2 is to calculate the 200th triangular number. See whether you can determine how the for statement works.

# Program 5.2

```
// Program to calculate the 200th triangular number
// Introduction of the for statement

#import <Foundation/Foundation.h>

int main (int argc, char * argv[])
{
    @autoreleasepool {
        int n, triangularNumber;

        triangularNumber = 0;

        for ( n = 1; n <= 200; n = n + 1 )
            triangularNumber += n;
```