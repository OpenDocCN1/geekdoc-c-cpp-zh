(3.31 \times 10^{-8} + 2.01 \times 10^{-7}) / (7.16 \times 10^{-6} + 2.01 \times 10^{-8})$

6. **Complex numbers** are numbers that contain two components: a *real* part and an *imaginary* part. If $a$ is the real component and $b$ is the imaginary component, this notation is used to represent the number:

$a + b i$

Write an Objective-C program that defines a new class called *Complex*. Following the paradigm established for the *Fraction* class, define the following methods for your new class:

```
- (void) setReal: (double) a;
-(void) setImaginary: (double) b;
-(void) print; // display as a + b
-(double) real;
-(double) imaginary;
```

Write a test program to test your new class and methods.

+   7. Suppose you are developing a library of routines to manipulate graphical objects. Start by defining a new class called **Rectangle**. For now, keep track of the rectangle's width and height. Develop methods to set the rectangle's width and height, retrieve these values, and calculate the rectangle's area and perimeter. Assume these rectangle objects describe rectangles on an integral grid, such as a computer screen. In that case, assume that the width and height of the rectangle are integer values.

Here is the @interface section for the Rectangle class: