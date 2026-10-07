# Chapter 3 Dealing with Data

Note the precedence and associativity rules come into play only when two operators share the same operand. Consider the following expression:
int dues = 20 * 5 + 24 * 6;

Operator precedence tells you two things:The program must evaluate 20 * 5 before adding them, and the program must evaluate 24 * 6 before adding. But neither precedence nor associativity says which multiplication takes place first. You might think that associativity goes to the leftmost multiplication first, but in this case, the * operators do not share a common operand, so the rules don't apply. In, C++ leaves it to the implementation to decide which order works best on a system. For this example, either order gives the same result, but there are circumstances in which the order can make a difference. You'll see one in Chapter 5, which discusses the increment operator.

# Division Diversions

You have to see the rest of the story about the division operator (/).The behavior of this operator depends on the type of the operands. If both are integers, C++ performs integer division.That means any fractional part of the result is discarded, making the result an integer. For this example, if one or both operands are floating-point, the fractional part is kept. Listing 3.11 illustrates how C++ division works with different types of values.As in Listing 3.10, Listing 3.11 invokes set() function to modify how the results are displayed.

# Listing 3.11 divide.cpp

```
// divide.cpp // integer and floating-point division
#include <iostream>
int main() {

using namespace std;

cout.setf(ios_base::fixed, ios_base::float);
cout << "Integer division: 9/5 = " << 9 / 5 << endl;
cout << "Floating-point division: 9.0/5.0 = " <<
cout << 9.0 / 5.0 << endl;
cout << "Mixed division: 9.0/5 = " << 9.0 / 5 << endl;
cout << "double constants: 1e7/9.0 = " <<
cout << 1.e7 / 9.0 << endl;
cout << "float constants: 1e7/9.0 = " <<
cout << 1.e7 / 9.0 << endl;

return 0;
}
```

Here is the output from the program in Listing 3.11 for one implementation:
Integer division: 9/5 = 1
Floating-point division: 9.0/5.0 = 1.800000
Mixed division: 9.0/5 = 1.800000