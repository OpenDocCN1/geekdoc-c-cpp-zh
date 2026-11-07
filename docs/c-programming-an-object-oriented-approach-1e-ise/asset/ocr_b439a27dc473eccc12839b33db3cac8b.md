![](bbox=[0.3, 0.08, 0.883, 0.15])

**Figure 3.7** Hierarchy of types for implicit conversion

# ## Implicit Type Change

After implicit promotion of each operand according to the rules we discussed above, the compiler may or may not perform implicit type change. **Implicit type change** occurs when the two operands are of different types; after the change, both operands are of the same type. If the operation is unary, there is no need for implicit conversion; if the operation is binary, the implicit type change may be needed to make the types of both operands the same. We discuss two cases.

**Expressions with No Side Effect** In this case, the operand in the lower level of hierarchy (smaller size) needs to be converted to the type of the higher level of hierarchy according to the hierarchy of types defined in Figure 3.7. Note that the types that are already promoted in the previous section are not included in this list. For example, data items of type bool, char, short, unsigned short, and float are not in this list because they are already implicitly promoted as described in the previous section.

The recipe followed by the compiler finds the operand with the higher level and converts the other one to that level.

# ### EXAMPLE 3.9

Program 3.9 shows an example. We have three variables.

**Program 3.9** Implicit type conversion (no side effect)

```
```cpp
/****************************************************************
 * Implicit type conversion in an expression of mixed types when
 * there is no side effect.
 ****************************************************************/
#include <iostream>
#include <typeinfo>
using namespace std;

int main ( )
{
    // Declarations
    int x = 123;
    long y = 140;
    double z = 114.56;
    // Check the type and value of expression x + y
    cout << "Type of x + y: " << typeid (x + y).name ()<<endl;
    cout << "Value of x + y: " << x + y << endl << endl;
```
```