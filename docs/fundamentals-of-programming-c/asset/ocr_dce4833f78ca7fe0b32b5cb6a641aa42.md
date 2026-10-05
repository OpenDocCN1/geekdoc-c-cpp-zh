# 4.1. EXPRESSIONS

Listing 4.3: imprecise10.cpp
#include <iostream>

using namespace std;

int main() {
  double one = 1.0,
  one_tenth = 1.0/10.0,
  zero = one - one_tenth - one_tenth - one_tenth
  - one_tenth - one_tenth - one_tenth
  - one_tenth - one_tenth - one_tenth;

  cout << "one = " << one << << "" , one_tenth = " << one_tenth
  << <<" , zero = " << zero << endl;
}

The program's output

```
one = 1, one_tenth = 0.1, zero = 1.38778e-06
```

Surely the reported answer (1.38778 × 10⁻⁶) is close to the correct answer (zero). If you rounded to the one-hundredth place (15 places after the decimal point), it is correct. Listing 5.5 (samifferent.cpp) in Chapter 5 emphasizes that the programmers must use care when dealing with the imprecision of floating-point numbers.

Despite their inexness, double-precision floating-point numbers are used day throughout the world to solve sophisticated scientific and engineering problems. The limitations of floating-point numbers are unavoidable when we do our best to represent values with infinite characteristics in a finite way. Floating-point numbers provide a good trade-off of precision for practicality.

Since a char is stored internally as a number (see Section 3.7), we can perform arithmetic on characters. We will have little to apply mathematics to characters, but sometimes it is useful. As an example, the lower-case letters of the alphabet–z are ASCII values 97–123, with a = 97, b = 98, etc. The upper-case letters A–Z are 65–91, with A = 65, B = 66, etc. To capitalize any lower-case letter, you need only subtract 32, as

```
char lower = 'd', upper = lower - 32;
cout << upper << endl;
```

This code would print D. If you do not remember the offset of 32 between upper- and lower-case, you can compute it with the themselves:

```
upper = lower - ('a' - 'A');
```

In this case, if lower has been assigned in the range 'a' to 'z', the statement will assign to the capitalized version of lower. On the other hand, if lower's value is outside of range, upper will not receive a meaningful value.