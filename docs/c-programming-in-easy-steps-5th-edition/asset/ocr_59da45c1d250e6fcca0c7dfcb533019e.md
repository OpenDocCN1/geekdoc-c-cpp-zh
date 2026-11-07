# Employing isolated classes

![](bbox=[0.118, 0.145, 0.189, 0.193])

ops.cpp

+   6. Start an implementation file with **include** directives for the header file created [here](#), and the standard C++ library supporting input/output statements.

```
```cpp
#include "ops.h"          // Reference header file.
#include <iostream>
using namespace std ;
```
```

+   7. Add the following definitions for each method in the header file, then save the implementation file as “ops.cpp”.

```
```cpp
Calculator::Calculator()
{ status = true ; }              // initialize status.

void Calculator::launch()       // Display instructions.
{
    cout << endl << "*** SUM CALCULATOR ***" << endl ;
    cout << "Enter a number, an operator(+,-,*)" << endl ;
         "another number." << endl << "Hit Return to
         calculate. Enter zero to exit." << endl ;
}

void Calculator::readInput()              // Get expression.
{
    cout << "> " ; cin >> num1 ;           // Get 1st number.
    if ( num1 == 0 ) status = false ;      // Exit if it's zero.
    else { cin >> oper ; cin >> num2 ; }   // Or get the rest.
}

void Calculator::writeOutput()             // Display result.
{
    if ( status ) switch( oper )            // If continuing.
    {
                                           // Show result.
        case '+' : { cout << ( num1 + num2 ) << endl ; break ; }
        case '-' : { cout << ( num1 - num2 ) << endl ; break ; }
        case '*' : { cout << ( num1 * num2 ) << endl ; break ; }
        case '/' : if ( num2 != 0 )
                       cout << ( num1 / num2 ) << endl ;
                   else cout << "Cannot divide by zero" << endl ;
    }
}

bool Calculator::run()                    // Get the current status.
{ return status ; }
```
```

![](bbox=[0.118, 0.733, 0.207, 0.794])

Due to space limitation, this program makes barely no attempt at input validation – it assumes the user will enter a valid expression, such as 8 * 3.

![](bbox=[0.118, 0.839, 0.19, 0.884])

sum.cpp

+   8. Start a client file with an include directive to incorporate the header file created [here](#).