# 16.2 STOPWATCH

```
int main() {
Rational f1(1, 2), f2(1, 3);
  cout << f1 << " + " << f2 << " = " << (f1 + f2) << endl;
  cout << f1 << " * " << f2 << " = " << (f1 * f2) << endl;
}
```

Listing 16.1 (rational.cpp) produces

![](bbox=[0.218, 0.247, 0.842, 0.323])

This rational number type has some notable features:

+   **Constructors.** The overloaded constructors permit convenient initialization and make it impossible to create an undefined fraction.

+   **Private static methods.** *Rational* provides two private static methods: *gcd* and *lcm*. The algorithm for the recursive *gcd* (greatest common divisor) method was introduced in Section 10.4. The *lcm* (least common multiple) method is derived from the mathematical relationship:

> gcd(m,n) × lcm(m,n) = m × n

These methods are declared private because they are not meant to be used by client code. Greatest common divisor and least common multiple are concepts from number theory of which *Rational* classes have no direct client. Client code expects functionality typical of rational numbers, such as addition and reduction; these two private methods are used by other, methods that provide functionality more closely related to rational numbers. These two methods are static because they do not use instance variables. An object is not required to compute the greatest common divisor of two integers. It is legal for *gcd* and *lcm* to be instance methods, instance methods should be used only when necessary, since they have the power to alter the state of an object. Faulty coding modifying an instance variable can be difficult to track. If a class is used, the compiler can stop any attempt to access an instance variable immediately.

+   **Public instance methods.** None of the instance methods (operator==, reduce, operator+, and operator*) modify the state of the object upon which they are invoked. The *Rational* class still produces immutable objects. The operator+, operator*, and reduce use the private helper methods to accomplish their respective tasks.

+   **Global** << operator operator<< is a global function that allows a *Rational* object to be to the cout object to be displayed conveniently as a built-in type.

# 16.2 Stopwatch

The linear search vs. binary search program (Listing 12.5 (searchcompare.cpp)) accessed the system clock in order to time the execution of a function. The program used the clock function from the standard C library and an additional variable to compute the elapsed time. The following skeleton code fragment: