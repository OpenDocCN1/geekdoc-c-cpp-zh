# 15.4 const Methods

Given the SimpleRational class in Listing 14.5 (simplerational.cpp), the following code produces a compiler error:

```
const SimpleRational fract(1, 2); // Constant fraction 1/2
fract.set_numerator(2); // Error, cannot change a constant
```

This behavior is desirable, since the set_numerator method can change the state of a SimpleRational object, and our fract object is supposed to be constant. Unfortunately, this correct behavior is accidental. The compiler does not analyze our methods to determine exactly what they do. Consider the following code that also will not compile:

```
const SimpleRational fract(1, 2); // Constant fraction 1/2
std::cout << fract.get_numerator(); // Error!
```

Since the get_numerator method does not modify a SimpleRational object, we would expect that invoking it on a constant object should be acceptable, but the compiler rejects it. Again, the compiler cannot understand what get_numerator is supposed to do; specifically, it is not designed to be able to determine that a method will not change the state of an object. The programmer must supply some additional information to help the compiler.

If a method is not supposed to change the state of an object, that method should be declared const. In the SimpleRational class, the methods get_numerator and get_denominator simply return, respectively, copies of the fraction’s numerator and denominator. Neither method is intended to modify any instance variables. If we look at the code for those methods, we see that indeed neither method changes anything about a SimpleRational object. What if the programmer made a mistake—perhaps a spurious copy and paste error—and the statement

```
numerator = 0;
```

made its way into the get_numerator method? Unfortunately, the way things stand now, the compiler cannot detect this error, and get_numerator will contain a serious logic error.

We can remove the possibility of such an error by declaring get_numerator (and get_denominator) const:

```
class SimpleRational {
public:
/* ... stuff omitted ... */
int get_numerator() const {
return numerator;
}
int get_denominator() const {
return denominator;
}
/* ... other stuff omitted ... */
};
```

The const keyword goes after the closing parenthesis of the parameter list and before the opening curly brace of the method’s body. If we accidentally attempt to reassign an instance variable in a const method, the compiler will report an error.