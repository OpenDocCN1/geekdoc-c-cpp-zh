# Exercises 67

2. Write a program that converts 27° from degrees Fahrenheit (F) to degrees Celsius
(C) using the formula:

C = (F - 32) / 1.8

Note that you don't need to define a class to perform this calculation. Simply eval-nuating the expression will suffice.

3. What output would you expect from the following program?
#import <Foundation/Foundation.h>

```
int main (int argc, char *argv[])
{
    NSAutleasePool * pool = [[NSAutleasePool alloc] init];
    char c, d;

    c = 'd';
    d = c;
    NSLog("@d = %c", d);

    [pool drain];
    return 0;
}
```

4. Write a program to evaluate the polynomial shown here (to calculate the expo-nents, there is no exponentiation operator in
Objective-C):
3x' - 5x' + 6
for x = 2.55

5. Write a program that evaluates the following expression and displays the results
(remember to use exponential format to display the result):

(3.31 * 10⁴ + 2.01 * 10¹) / (7.16 * 10⁴ + 2.01 * 10⁴)

6. Complex numbers have two components: a real part and an
imaginary part. If a is the real component and b is the imaginary component, then
notation is used to represent the number:

a + bi

Write an Objective-C program that defines a new class called Complex. Following
t paradigm established for the Fraction class, define the following methods for
your class:

+   - (void) setReal:(double) a;
- (void) setImaginary:(double) b;
- (void) print(); // display as a + bi
- (double) real;
- (double) imaginary;

Write test program to test your new class and methods.