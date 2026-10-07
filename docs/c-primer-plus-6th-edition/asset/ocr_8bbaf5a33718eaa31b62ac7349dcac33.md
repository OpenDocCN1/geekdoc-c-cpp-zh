The constructor itself can be used as an argument to functions such as count_if:
count3 = std::count_if(numbers.begin(), numbers.end(), f_mod(3));

The argument f_mod(3) creates the value 3, and count_if() uses the created object to call the operator() method, setting the parameter x equal to an element of numbers. To count how many numbers are divisible by 13 instead of use
f_mod(13) as the third argument.

Finally, let's examine the lambda approach. The name comes from lambda calculus, a mathematical system for defining and applying functions. The system enables one to use anonymous functions—that is, it allows one to dispense with function names. In C++11 context, you can use an anonymous function definition (a lambda) as an argument to functions using a function pointer. The lambda corresponding to the f3() function is:

```
[] (int x) { return x % 3 == 0 };
```

It looks like the definition of f3:

```
bool f3(int x) { return x % 3 == 0 };
```

The two differences are that the function name is replaced with [] (how anonymous is that!) and there is no declared return type. Instead, the return type is deduced decltype from the return value, which would be bool in this case. If the lambda has no return statement, the type is deduced to void. In our example, you would use this lambda as follows:

```
count3 = std::count_if(numbers.begin(), numbers.end(),
[](int x) { return x % 3 == 0 });
```

That is, you use the entire lambda expression as you would use a pointer or a functor constructor.

The automatic deduction for lambdas works only if the body consists of a single return statement. Otherwise, you need to use the trailing-return-value syntax:
[] (double x, int y) -> double { return x - y }; // return type is double

Listing 18.4 illustrates the points just discussed.

# Listing 18.4 lambda0.cpp

```
// lambda0.cpp using lambda expressions
#include <iostream>
#include <vector>
#include <algorithm>
#include <cmath>
#include <ctime>
const long Size1 = 39L;
const long Size2 = 100*Size1;
const long Size3 = 100*Size2;
```