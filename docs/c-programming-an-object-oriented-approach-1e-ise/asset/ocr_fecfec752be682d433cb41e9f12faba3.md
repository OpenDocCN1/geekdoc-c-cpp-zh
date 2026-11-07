**Table 12.1  Operation on type_info objects**

| Expression | Operation |
|---|---|
| `t1 == t2` | Return true if t1 and t2 are of the same type |
| `t1 != t2` | Return true if t1 and t2 are of different types |
| `t1.name()` | Returns a C-type string (name of the t1) |
| `t1.before(t2)` | Returns true if t1 comes before t2 (in inheritance) |

during the compilation. For example, when, during program execution, different objects are being inserted into a polymorphic variable and the program needs to call the appropriate function, then the binding must be done during run time. For this reason, we need a virtual function to force the run-time system to create a table that shows which object needs which function and to bind the call to the appropriate function. Polymorphism is closely tied to dynamic binding because we want to be able to execute the appropriate function definition.

# 12.1.4 Run-Time Type Information (RTTI)

When working with hierarchy of classes, sometimes we need to know the type of the object we are dealing with or sometimes we want to change the type of the object.

# Using typeid Operator

If we want to find the type of the object at run time, we can use the `<typeinfo>` header to access an object of the class *type_info* (note that the class name has an underscore, but the header name does not). The class *type_info* has no constructor, destructor, or copy constructor. The only way to create an object of type *type_info* is by using an overloaded operator named *typeid*. We can create an object of *type_info* by passing an expression to the operator *typeid* that can be evaluated as a type; for example, *typeid* (5), *typeid* (object_name), *typeid* (6 + 2), and so on. We can then use one of the four member functions or operators that are defined in the *type_info* class as shown in Table 12.1, in which t1 and t2 are objects of *type_info* class.

Program 12.9 shows how we can find the type of two objects.

```
```cpp
/************************************************************
 * A program to use typeid operator to find the name of classes   *
 ************************************************************/
#include <iostream>
#include <string>
#include <typeinfo>
using namespace std;

class Animal {};
class Horse {};

int main ( )
{
```
```

(continued)