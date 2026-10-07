# Data Types and Constants

Program 4.1
#import <Foundation/Foundation.h>

```
int main (int argc, char *argv[])
{
    NSAutleasePool * pool = [NSAutleasePool alloc] init];

    int integerVar = 100;
    float floatingVar = 331.79;
    double doubleVar = 8.44e+11;
    char charVar = 'W';

    NSLog("%i", integerVar);
    NSLog("%f", floatingVar);
    NSLog("%e", doubleVar);
    NSLog("%g", doubleVar);
    NSLog("%c", charVar);

    [pool drain];
    return 0;
}
```

# Program 4.1 Output

```
integerVar = 100
floatingVar = 331.790009
doubleVar = 8.440000e+11
doubleVar = 8.44e+11
charVar = W
```

In the second line of the program's output, notice that the value of 331.79, which is assigned to floatingVar, is actually displayed as 331.790009. The reason for this inaccuracy is the particular range in which numbers are internally represented inside the computer. You have probably noticed this inaccuracy when you divide 1 by 3 on your calculator, you get the result .3333333 with some additional 3s tacked on the end. The string of 3s is the calculator's approximation to one third. Theoretically, there should be an infinite number of 3s. But the calculator can only hold so many digits, so the inherent inaccuracy of the machine. The type of inaccuracy applies here: Certain floating-point values cannot be exactly represented inside the computer's memory.

# Qualifiers: long, long, short, unsigned, and signed

If the qualifier long is placed directly before the int declaration, the declared integer variable is of extended range on some computer systems. An example of a long int declaration might be this:
long int factorial;

This declares the variable factorial to be a long integer variable. As floats and doubles, the particular range of a long variable depends on your particular computer system.