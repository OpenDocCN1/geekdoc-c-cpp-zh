# 7. More on Classes

In this chapter, you'll continue learning how to work with classes and write methods. You'll also apply some of the concepts you learned in the previous chapter, such as completing program looping, making decisions, and working with expressions. First we talk about splitting your program into multiple files to make working with larger programs easier.

# Separate Interface and Implementation Files

It's time to get used to putting your class declarations and definitions in separate files.

If you're using Xcode, start a new project called FractionTest. Type the following program into the file main.m:

# Program 7.1. Main Test Program: main.m

```
#import "Fraction.h"

int main (int argc, char * argv[]) {
    @autoreleasepool {
        Fraction *myFraction = [[Fraction alloc] init];

        // set fraction to 1/3

        [myFraction setNumerator: 1];
        [myFraction setDenominator: 3];
    }
```