# CHAPTER 4 Parameters and Overloading

Display 4.3 Comparing Argument Mechanisms (part 2 of 2)

| 22 | cout << "parValue in function call = " |
| 23 | << par1Value << endl; |
| 24 | par2Ref = 222; |
| 25 | cout << "par2Ref in function call = " |
| 26 | << par2Ref << endl; |
| 27 | } |

Sample Dialogue

```
parValue in function call = 111
par2Ref in function call = 222
n1 after function call = 1
n2 after function call = 222
```

![](bbox=[0.125, 0.413, 0.203, 0.455])

> PITFALL: Inadvertent Local Variables

If you want to change the value of a variable, the corresponding formal parameter must be a call-by-reference parameter and must have the ampersand, &, attached to its type. If you carelessly omit the ampersand, the function will have a call-by-value parameter where you meant to have a call-by-reference parameter. When the program runs, you will discover that the function call does not change the value of the corresponding argument, because a formal call-by-value parameter is a local variable. If the variable has its value changed in the function, then, with any local variable, that change has no effect outside the function body. This is an error that can be very difficult to see because the code looks right.
For example, the program in Display 4.4 is similar to the program in Display 4.2 except that the parameters were mistakenly omitted from the function arguments. As a result, the arguments firstNum and secondNum are local variables. The argument firstNum and secondNum are never substituted in variable1 and variable2; variable1 and variable2 are instead initialized to the value of firstNum and secondNum. Then, the values of variable1 and variable2 are exchanged. The omission of two ampersands has the program completely wrong, yet it looks identical to the correct program and will compile and run without any errors.

Display 4.4 Inadvertent Local Variable (part 1 of 2)

```
//Program to demonstrate call-by-reference parameters.
#include <iostream>
using namespace std;

void getNumbers(int& input1, int& input2);
//Reads two integers from the keyboard.
```