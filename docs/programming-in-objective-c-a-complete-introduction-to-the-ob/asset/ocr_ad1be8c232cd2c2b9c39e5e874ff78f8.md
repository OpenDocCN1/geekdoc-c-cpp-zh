# Arithmetic Expressions

produces the intermediate result of 21. Finally, adding the remainder of dividing a b by d, as indicated by the expression a % d, leads to the final result of 25. There is no coincidence this value is the same as the value of the variable a. In general, this expression will always equal the value of a, assuming, of course, that a and b are both integer values:

```
a / b * b + a % b
```

In fact, the modulus operator % is defined to work only with integer values. As far as precedence is concerned, the modulus operator has equal precedence to the multiplication and division operators. This, of course, that an expression such as table + value % TABLE_SIZE

will be evaluated

```
table + (value % TABLE_SIZE)
```

# Integer and Floating-Point Conversions

To develop Objective-C programs, you must understand the rules used for the implicit conversion of floating-point and integer values in Objective-C. Program 4.5 demonstrates some of the simple conversions between numeric data types.

Program 4.5

// Basic conversions in Objective-C

```
//import <Foundation/Foundation.h>
```

```
int main (int argc, char *argv[]) {
    NSAutoreleasePool *pool = [NSAutoreleasePool alloc] init];n    float f1 = 123.25, f2;
    int i1, i2 = -150;

    i1 = f1; // floating to integer conversion
    NSLog("%f assigned to an int produces %i", f1, i1);

    f2 = i2; // integer to floating conversion
    NSLog("%i assigned to a float produces %f", i2, f2);

    f1 = i2 / 100; // integer divided by integer
    NSLog("%d divided by 100 produces %f", i2, f1);

    f2 = (float)i2 / 100.0; // integer divided by a float
    NSLog("%d divided by 100.0 produces %f", i2, f2);

    [pool drain];
    return 0;
}
```