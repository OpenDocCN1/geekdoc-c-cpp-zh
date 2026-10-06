conditions. I will go swimming if it is not raining. Similarly, in the program statement

```
if ( count > MAXIMUM_SONGS )
  [playlist maxExceeded];
```

the maxExceeded message is sent to playlist only if the value of count is greater than the value of MAXIMUM_SONGS; otherwise, it is ignored.

An actual program example will drive the point home. Suppose you want to write a program that accepts an integer entered from the keyboard and then displays the absolute value of that integer. A straightforward way to calculate the absolute value of an integer is to simply negate the number if it is less than zero. The phrase “if it is less than zero” in the previous sentence signals that the program must make a decision. This decision can be affected by the use of an if statement, as shown in the program that follows.

# Program 6.1

```
// Calculate the absolute value of an integer

#import <Foundation/Foundation.h>

int main (int argc, char * argv[]) {
  @autoreleasepool {
    int number;

    NSLog (@"Type in your number: ");\n    scanf("%i", &number);

    if ( number < 0 )
      number = -number;
  }
```