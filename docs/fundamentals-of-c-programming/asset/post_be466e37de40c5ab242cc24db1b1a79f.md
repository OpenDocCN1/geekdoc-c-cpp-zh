
(b) If a client creates 100 ValType objects, how many value2 fields will exist in memory?

## 11. How is a C++ struct similar to a class?

## 12. How does a C++ struct differ from a class?

## 13. Given the following custom type declarations:

```cpp
class X {
    int value1;
public:
    static int value2;
    int value3;
    X() : value1(5) {}
    void f() {
        value1 = 0;
    }
    static void g() {
        value2 = 0;
    }
};
int X::value2 = 3;
```

```cpp
struct Y {
    int quantity1;
    Y() : quantity1(5) {}
    void f() {
        quantity1 = 0;
    }
private:
    int quantity2;
};
```

and the following variable declarations:

```cpp
X x_obj;
Y y_obj;
```

determine if each of the following statements is legal.

- (a) x_obj.value1 = 0;
- (b) x_obj.value2 = 0;
- (c) x_obj.value3 = 0;
- (d) X::value1 = 0;
- (e) X::value2 = 0;
- (f) X::value3 = 0;
- (g) y_obj.quantity1 = 0;
- (h) y_obj.quantity2 = 0;
- (i) Y::quantity1 = 0;
- (j) Y::quantity2 = 0;
- (k) x_obj.f();
- (l) x_obj.g();
- (m) X::f();
- (n) X::g();

## 14. What privileges does function f have with respect to the class that declares f to be its friend?

## 15. Consider the following class declaration:

```cpp
class ValType {
int value;
public:
ValType() : value(0) {}
void set(int v1) {
value = v1;
}
void show() const {
std::cout << value << '\n';
}
friend int f(const ValType& x);
};
```

and determine the legality of each of the following function definitions:

- (a) int f(const ValType& x) {
    return 2 * x.value;
  }

- (b) int g(const ValType& x) {
    return 2 * x.value;
  }

- (c) int f(const ValType& x) {
    x.show();
    return 0;
  }

- (d) int g(const ValType& x) {
    x.show();
    return 0;
  }

- (e) int f(const ValType& x, int n) {
    return n * x.value;
  }

## 16. What are the risks associated with using the friend construct?

## Chapter 16

### Building some Useful Classes

This chapter uses the concepts from the past few chapters to build some complete, practical classes.

## 16.1 A Better Rational Number Class

Listing 16.1 (rational.cpp) enhances the SimpleRational class (Listing 14.5 (simplerational.cpp)) providing a more complete type.

### Listing 16.1: rational.cpp

```cpp
#include <iostream>

class Rational {
 int numerator;
 int denominator;

 // Compute the greatest common divisor (GCD) of two integers
 static int gcd(int m, int n) {
   if (n == 0)
     return m;
   else
     return gcd(n, m % n);
 }

 // Compute the least common multiple (LCM) of two integers
 static int lcm(int m, int n) {
   return m * n / gcd(m, n);
 }

 public:
 Rational(int n, int d): numerator(n), denominator(d) {
   if (d == 0) { // Disallow an undefined fraction
     std::cout << "*****Warning---Illegal Rational\n";
     numerator = 0; // Make up a reasonable default fraction
     denominator = 1;
   }
 }

 // Default fraction is 0/1
 Rational(): numerator(0), denominator(1) {}

 int get_numerator() const {
     return numerator;
 }

 int get_denominator() const {
     return denominator;
 }

 Rational reduce() const {
     // Find the factor that numerator and denominator have in common...
     int factor = gcd(numerator, denominator);
     // ...then divide it out in the new fraction
     // return Rational(numerator/factor, denominator/factor);
     return {numerator/factor, denominator/factor};
 }

 // Equal fractions have identical numerators and denominators
 bool operator==(const Rational& fract) const {
     // First, find the reduced form of this fraction and the parameter...
     Rational f1 = reduce(),
              f2 = fract.reduce();
     // ...then see if their components match.
     return (f1.numerator == f2.numerator)
         && (f1.denominator == f2.denominator);
 }

 // Unequal fractions are not equal
 bool operator!=(const Rational& other) {
     return !(*this == other);
 }

 // Compute the sum of fract and the current rational number
 Rational operator+(const Rational& fract) const {
     // Find common denominator
     int commonDenominator = lcm(denominator, fract.denominator);
     // Add the adjusted numerators
     int newNumerator = numerator * commonDenominator/denominator
         + fract.numerator * commonDenominator/fract.denominator;
     return {newNumerator, commonDenominator};
 }

 // Compute the product of fract and the current rational number
 Rational operator*(const Rational& fract) const {
     return Rational(numerator * fract.numerator,
         denominator * fract.denominator).reduce();
 }
};

// Allow a Rational object to be displayed in a nice
// human-readable form.
std::ostream& operator<<(std::ostream& os, const Rational& r) {
    os << r.get_numerator() << "/" << r.get_denominator();
    return os;
}
int main() {
Rational f1(1, 2), f2(1, 3);
std::cout << f1 << " + " << f2 << " = " << (f1 + f2) << '\n';
std::cout << f1 << " * " << f2 << " = " << (f1 * f2) << '\n';
}
```

Listing 16.1 (rational.cpp) produces

```
1/2 + 1/3 = 5/6
1/2 * 1/3 = 1/6
```

This rational number type has some notable features:

- **Constructors**. The overloaded constructors permit convenient initialization and make it impossible to create an undefined fraction.

- **Private static methods**. Rational provides two `private static` methods: `gcd` and `lcm`. The algorithm for the recursive `gcd` (greatest common divisor) method was introduced in Section 10.5. The `lcm` (least common multiple) method is derived from the mathematical relationship:

gcd(m,n) x lcm(m,n) = m x n

These two methods are declared `private` because they are not meant to be used directly by client code. *Greatest common divisor* and *least common multiple* are concepts from number theory which `Rational` clients have no direct need. Client code expects functionality typical of rational numbers, such as addition and reduction; these two private methods are used by other, public, methods that provide functionality more closely related to rational numbers. These two private methods are `static` methods because they do not use instance variables. An object is not required to compute the greatest common divisor of two integers. It is legal for `gcd` and `lcm` to be instance methods, but instance methods should be used only where necessary, since they have the power to alter the state of an object. Faulty coding that accidentally modifies an instance variable can be difficult to track down. If a class method is used, however, the compiler can spot any attempt to access an instance variable immediately.

- **Public instance methods**. None of the instance methods (`operator==`, `reduce`, `operator+`, and `operator*`) modify the state of the object upon which they are invoked. Thus, the `Rational` class still produces immutable objects. The methods `operator+`, `operator*`, and `reduce` use the `private` helper methods to accomplish their respective tasks.

- **Global << operator**. `operator<<` is a global function that allows a `Rational` object to be sent to the `std::cout` object to be displayed as conveniently as a built-in type.

## 16.2 Stopwatch

The linear search vs. binary search comparison program (Listing 12.5 (searchcompare.cpp)) accessed the system clock in order to time the execution of a section of code. The program used the `clock` function from the standard C library and an additional variable to compute the elapsed time. The following skeleton code fragment:

```cpp
clock_t seconds = clock(); // Record starting time
/*
 * Do something here that you wish to time
 */
clock_t other = clock(); // Record ending time
std::cout << static_cast<double>(other - seconds) / CLOCKS_PER_SEC
          << " seconds\n";
```

certainly works and can be adapted to any program, but it has several drawbacks:

- A programmer must take care to implement the timing code correctly for each section of code to be timed. This process is error prone:
  - clock_t is a specialized type that is used infrequently. It is not obvious from its name that clock_t is equivalent to an unsigned integer, so a programmer may need to consult a library reference to ensure its proper use.
  - The programmer must specify the correct arithmetic:
    (other - seconds)/CLOCKS_PER_SEC
  - The type cast to double of the time difference is necessary but easily forgotten or applied incorrectly. If a programmer incorrectly applies parentheses as so
    static_cast<double>((other - seconds)/CLOCKS_PER_SEC)
    the result will lose precision. Worse yet, the following parenthetical grouping
    static_cast<double>(other) - seconds/CLOCKS_PER_SEC
    will result in an invalid value, since division has precedence over subtraction.
- The timing code is supplemental to the actual code that is being profiled, but it may not be immediately obvious by looking at the complete code which statements are part of the timing code and which statements are part of the code to be timed.

Section 10.6 offered a solution to the above shortcomings of using the raw types, constants, and functions available from the C time library. Listing 10.14 (timemodule.cpp) hides the details of the C time library and provides a convenient functional interface to callers. Unfortunately, as mentioned in Section 10.6, the functional approach has a serious limitation. The code in Listing 10.14 (timemodule.cpp) uses global variables to maintain the state of the timer. There is only one copy of each global variable. This means programmers using the timer functions cannot independently measure the elapsed time of overlapping events; for example, you cannot measure how long it takes for a function to execute and simultaneously measure how long a section of code within that function takes to execute.

A programmer could time multiple, simultaneous activities by using the raw C library clock function directly, but then we are back to where we began: messy, potentially error-prone code.

Objects provide a solution. Consider the following client code that uses a stopwatch object to keep track of the time:

```cpp
Stopwatch timer; // Declare a stopwatch object
timer.start(); // Start timing
```
