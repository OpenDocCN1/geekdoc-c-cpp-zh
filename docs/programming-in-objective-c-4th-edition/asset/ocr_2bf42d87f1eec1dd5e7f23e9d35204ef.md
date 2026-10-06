basic data types in these arrays. Instead, to store any of the basic numeric data types (including the char data type), you can use the NSNumber class to create objects from these data types. (See Program 15.1.)

# Program 15.1

```
// Working with Numbers

#import <Foundation/Foundation.h>

int main (int argc, char * argv[]) {
    @autoreleasepool {
        NSNumber *myNumber;
        *floatNumber, *intNumber;
        NSInteger myInt;

        // integer value
        intNumber = [NSNumber numberWithInteger:100];
        myInt = [intNumber integerValue];
        NSLog("%@li", (long) myInt);

        // long value
        myNumber = [NSNumber numberWithLong:0xabcdef];
        NSLog("%@lx", [myNumber longValue]);

        // char value
        myNumber = [NSNumber numberWithChar:
```