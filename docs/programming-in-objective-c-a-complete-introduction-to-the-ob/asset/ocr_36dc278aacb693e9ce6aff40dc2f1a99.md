# The Modulus Operator

The last arithmetic operator to be presented in this chapter is the modulus operator, which is symbolized by the percent sign (%). Try to determine how this operator works by analyzing the output from Program 4.4.

Program 4.4

```
// The modulus operator

#import <Foundation/Foundation.h>

int main (int argc, char *argv[]) {
    NSAutleasePool *pool = [NSAutleasePool alloc init];
    int a = 25, b = 5, c = 10, d = 7;

    NSLog("%%a %% b = %i", a, b);
    NSLog("%%a %% c = %i", a, c);
    NSLog("%%a %% d = %i", a, d);
    NSLog("%%a / d * d + a %% d = %i", a, d * d + a % d);

    [pool drain];
    return 0;
}
```

# Program 4.4 Output

a % b = 0
a % c = 5
d % d = 4
a / d * d + a % d = 25

The statement inside main that defines and initializes the variables a, b, c, and d in a single statement.
As know, NSLog uses the character that immediately follows the percent sign to determine how to print its next argument. However, if it is another percent sign follows, the NSLog routine takes this as an indication that you really intend to display a percent sign and inserts it at the appropriate place in the program's output.
You are correct if you concluded that the function of the modulus operator is to give the remainder of the first value divided by the second. In the first example, the remainder of 25 divided by 5 is displayed as 0. If you divide 25 by 10, you get a remainder of 5, as verified by the second line of output. Dividing 7 by 7 gives a remainder of 4, as shown in the third output line.
Let's now turn attention to the last arithmetic expression evaluated in the last statement. We will recall that any operations between two integer values in Objective-C are performed with integer arithmetic. Therefore, any resulting from the division of two integer values is simply discarded. Dividing 25 by 7, as indicated by the expression a / d, gives an intermediate result of 3. Multiplying this value by the value of d, which is 7,