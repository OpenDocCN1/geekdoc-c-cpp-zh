# Answers to Self-Review Exercises

**9.1** a) dot (.), arrow (->), b) private. c) public. d) Default memberwise assignment (performed by the assignment operator).

+   **9.2**
+   
+    a) *Error:* Destructors are not allowed to return values (or even specify a return type) or take arguments.
+   
+    *Correction:* Remove the return type `void` and the parameter `int` from the declaration.
+   
+    b) *Error:* Members cannot be explicitly initialized in the class definition.
+   
+    *Correction:* Remove the explicit initialization from the class definition and initialize the data members in a constructor.
+   
+    c) *Error:* Constructors are not allowed to return values.
+   
+    *Correction:* Remove the return type from the declaration.

# Exercises

**9.3** *(Scope Resolution Operator)* What’s the purpose of the scope resolution operator?

**9.4** *(Enhancing Class Time)* Provide a constructor that’s capable of using the current time from the time and localtime functions—declared in the C++ Standard Library header `<ctime>`—to initialize an object of the `Time` class.

**9.5** *(Complex Class)* Create a class called Complex for performing arithmetic with complex numbers. Write a program to test your class. Complex numbers have the form

```
realPart + imaginaryPart * i
```

where i is

```
√−1
```

Use double variables to represent the private data of the class. Provide a constructor that enables an object of this class to be initialized when it’s declared. The constructor should contain default values in case no initializers are provided. Provide public member functions that perform the following tasks:

+   a) Adding two Complex numbers: The real parts are added together and the imaginary parts are added together.
+   
+   b) Subtracting two Complex numbers: The real part of the right operand is subtracted from the real part of the left operand, and the imaginary part of the right operand is subtracted from the imaginary part of the left operand.
+   
+   c) Printing Complex numbers in the form (a, b), where a is the real part and b is the imaginary part.

**9.6** *(Rational Class)* Create a class called Rational for performing arithmetic with fractions. Write a program to test your class.

Use integer variables to represent the private data of the class—the numerator and the denominator. Provide a constructor that enables an object of this class to be initialized when it’s declared. The constructor should contain default values in case no initializers are provided and should store the fraction in reduced form. For example, the fraction

```
\frac{2}{4}
```

would be stored in the object as 1 in the numerator and 2 in the denominator. Provide public member functions that perform each of the following tasks:

+   a) Adding two Rational numbers. The result should be stored in reduced form.
+   
+   b) Subtracting two Rational numbers. The result should be stored in reduced form.
+   
+   c) Multiplying two Rational numbers. The result should be stored in reduced form.