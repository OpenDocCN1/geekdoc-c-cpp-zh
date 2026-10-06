```
// Simple program to work with fractions

#import <Foundation/Foundation.h>

int main (int argc, char * argv[])
{
    @autoreleasepool {
        int numerator = 1;
        int denominator = 3;
        NSLog (@"The fraction is %i/%i",
        numerator, denominator);
    }
    return 0;
}
```

# Program 3.1. Output

The fraction is 1/3

In Program 3.1 the fraction is represented in terms of its numerator and denominator. After the @autoreleasepool directive, the two lines in main both declare the variables numerator and denominator as integers and assign them initial values of 1 and 3, respectively. This is equivalent to the following lines:

```
int numerator, denominator;
```

numerator = 1;
denominator = 3;

We represented the fraction 1/3 by storing 1 in the variable numerator and 3 in the variable denominator. If you needed to store a lot of fractions in your program, this could be cumbersome.