# The if Statement

The second if statement tests the remainder to see if it's not equal to zero, and if that's the case, displays a message stating that the number is odd.

Whenever the first statement succeeds, the second one must fail, and vice versa. When you recall from our discussions of even/odd numbers at the beginning of this section, we said that if the number is divisible by 2, it is even; otherwise, it is odd.

When writing programs, this "else" concept is so frequently required that a special construct is provided to handle this situation. In Objective-C, this is known as the if-else, and the general format is as follows:

```
if ( expression )
    program statement 1
else
    program statement 2
```

The if-else is actually just an extension of the general format of the if statement. The result of the expression's evaluation is true, then program statement 1, which immediately follows, is executed; otherwise, program statement 2 is executed. In either case, either program statement 1 or program statement 2 will be executed, but not both.

You can incorporate the if-else statement into the previous program, replacing the two statements by a single if-else statement. You will see how this new program construct actually reduces the program's complexity somewhat and improves its readability.

# Program 6.4

```
// Determine if a number is even or odd (Ver. 2)

#import <Foundation/Foundation.h>

int main (int argc, char *argv[]) {
    NSAutleasePool *pool = [[NSAutleasePool alloc] init];
    int number_to_test, remainder;

    NSLog("@Enter your number to be tested:");
    scanf("%i", &number_to_test);

    remainder = number_to_test % 2;
    if (remainder == 0) {
        NSLog("@The number is even.");
    } else {
        NSLog("@The number is odd.");
    }

    [pool drain];
    return 0;
}
```