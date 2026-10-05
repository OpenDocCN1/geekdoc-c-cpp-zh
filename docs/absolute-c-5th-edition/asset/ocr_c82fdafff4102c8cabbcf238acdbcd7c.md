# CHAPTER 3 Function Basics

Display 3.1 A Predefined Function That Returns a Value

```
//Computes the size of a doghouse that can be purchased
//given the user's budget.
#include <iostream>
#include <cmath>
using namespace std;

int main() {
    const double COST_PER_SQ_FT = 10.50;
    double budget, area, lengthSide;

    cout << "Enter the amount budgeted for your doghouse $\$\
```

Sample Dialogue

| Enter the amount budgeted for your doghouse $25.00 |
| For a price of $25.00 |
| I can build you a luxurious doghouse |
| that is 1.54 feet on each side. |

Usually, all you need to use a library is to place an include directive and a using directive for library in the file with your program. If you work with just these directives, you need not to worry about doing anything else. However, for some libraries on some systems you may need to give additional instructions to the compiler or explicitly run a linker program to link the library. The details vary from one system to another; you will have to check your manual or ask a local expert to see exactly what is necessary.

A few predefined functions are described in Display 3.2. More predefined functions are described in Appendix 4. Notice that the absolute value functions abs and labs are