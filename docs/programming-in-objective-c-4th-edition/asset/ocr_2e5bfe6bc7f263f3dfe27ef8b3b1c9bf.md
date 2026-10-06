```
#import <Foundation/Foundation.h>

int main (int argc, const char *argv[]) {
    @autoreleasepool {
        int sum;

        sum = 50 + 25;
        NSLog("The sum of 50 and 25 is %i", sum);
    }

    return 0;
}
```

# Program 2.4. Output

The sum of 50 and 25 is 75

The first program statement inside main after the autorelease pool sets up define the variable sum to be of integer. You must define all program variables before you can use them in a program. The definition of a variable specifies to the Objective-C compiler how the program should use it. The compiler needs this information to generate the correct instructions to store and retrieve values into and out of the variable. A variable defined as type int can be used to hold only integral values—that is, values without decimal places. Examples of integral values are 3, 5, -20, and 0. Numbers with decimal places, such as 2.14, 2.455, and 27.0, are known as floating-point numbers and are real numbers.