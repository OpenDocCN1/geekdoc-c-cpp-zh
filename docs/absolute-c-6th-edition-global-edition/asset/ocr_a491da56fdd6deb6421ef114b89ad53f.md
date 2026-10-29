number you started out with. For example, the square root of 9 is 3 because 3² is equal to 9.) The function sqrt starts with a number, such as 9.0, and computes its square root, in this case 3.0. The value the function starts out with is called its argument. The value it computes is called the value returned. Some functions may have more than one argument, but no function has more than one value returned.

The syntax for using functions in your program is simple. To set a variable named theRoot equal to the square root of 9.0, you can use the following assignment statement:

```
theRoot = sqrt(9.0);
```

The expression sqrt(9.0) is known as a function call or function invocation. An argument in a function call can be a constant, such as 9.0, a variable, or a more complicated expression. A function call is an expression that can be used like any other expression. For example, the value returned by sqrt is of type double; therefore, the following is legal (although perhaps stingy):

```
bonus = sqrt(sales)/10;
```

sales and bonus are variables that would normally be of type double. The function call sqrt(sales) is a single item, just as if it were enclosed in parentheses. Thus, the previous assignment statement is equivalent to

```
bonus = (sqrt(sales))/10;
```

You can use a function call wherever it is legal to use an expression of the type specified for the value returned by the function.

Display 3.1 contains a complete program that uses the predefined function sqrt. The program computes the size of the largest square doghouse that can be built for the amount of money the user is willing to spend. The program asks the user for an amount of money and then determines how many square feet of floor space can be purchased for that amount. That calculation yields an area in square feet for the floor of the doghouse. The function sqrt yields the length of one side of the doghouse floor.

The cmath library contains the definition of the function sqrt and a number of other mathematical functions. If your program uses a predefined function from some library, then it must contain an include directive that names that library. For example, the program in Display 3.1 uses the sqrt function and so it contains

```
#include <cmath>
```

This particular program has two include directives. It does not matter in what order you give these two include directives. include directives were discussed in Chapter 1.

Definitions for predefined functions normally place these functions in the std namespace and so also require the following using directive, as illustrated in Display 3.1:

```
using namespace std;
```

argument value returned

function call or function invocation

#include directive