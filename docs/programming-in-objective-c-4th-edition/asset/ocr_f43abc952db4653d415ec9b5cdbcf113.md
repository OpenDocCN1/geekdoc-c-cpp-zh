a * b + c * d

is evaluated according to the rules stated previously as

(a * b) + (c * d)

or

(100 * 2) + (25 * 4)

The result of 300 is handed to the NSLog routine.

# Integer Arithmetic and the Unary Minus Operator

Program 4.3 reinforces what we have just discussed and introduces the concept of integer arithmetic.

# Program 4.3 arithmetic expressions

```
// More arithmetic <Foundation/Foundation.h>
#import <Foundation/Foundation.h>

int main(int argc, char * argv[]) {
    @autoreleasepool {
        int a = 25;
        int b = 2;
        float c = 25.0;
        float d = 2.0;
    }

    NSLog ("%6 + a / 5 * b = %i", 6 + a / 5 *);
    NSLog ("@%a / b * b = %i", a / b * b);
    NSLog ("@%c / d * d = %f", c / d * d);
```