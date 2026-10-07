# Program 15.1

// Working with Numbers

```
#import <Foundation/Foundation.h>

int main (int argc, char *argv[])\{
    NSAutoreleasePool *pool = [[NSAutoreleasePool alloc] init];
    NSNumber *myNumber, *floatNumber, *intNumber;
    NSInteger myInt;

    // integer value
    intNumber = [NSNumber numberWithInteger: 100];
    myInt = [intNumber integerValue];
    NSLog("@%lx", (long) myInt);

    // long value
    myNumber = [NSNumber numberWithLong: 0xabcdef];
    NSLog("@%lx", [myNumber longValue]);

    // char value
    myNumber = [NSNumber numberWithChar: 'X'];
    NSLog("@%c", [myNumber charValue]);

    // float value
    floatNumber = [NSNumber numberWithFloat: 100.00];
    NSLog("@%g", [floatNumber floatValue]);

    // double value
    myNumber = [NSNumber numberWithDouble: 12345e+15];
    NSLog("@%lg", [myNumber doubleValue]);

    // Wrong access here\
    NSLog("@%li", (long) [myNumber integerValue]);

    // Test two numbers for equality
    if ([intNumber isEqualToNumber:floatNumber] == YES)
        NSLog("@*Numbers are equal");
    else
        NSLog("@*Numbers are not equal");

    // Test if one number is <, ==, or > second
    if ([intNumber compare:myNumber] == NSOrderedAscending)
        NSLog("@*First number is less than second");

    [pool drain];
    return 0;
}
```