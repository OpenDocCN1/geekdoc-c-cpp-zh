Program 5.4 asks the user which triangular number should be calculated, calculates that number, and then displays the results.

# Program 5.4

```
#import <Foundation/Foundation.h>

int main (int argc, char * argv[]) {
    @autoreleasepool {
        int n, number, triangularNumber;

        NSLog ("@What triangular number do you want?");
        scanf("%i", &number);

        triangularNumber = 0;

        for ( n = 1; n <= number; ++n) {
            triangularNumber += n;
        }

        NSLog ("@Triangular number %i is %i\n", number, triangularNumber);
    }

    return 0;
}
```

In the program output follows, the number typed by the user **(100)** is set in bold type, to distinguish it from the output displayed by the program.

# Program 5.4. Output