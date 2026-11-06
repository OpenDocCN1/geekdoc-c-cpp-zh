**Software Engineering Observation 10.8**

Even though the prototypes for friend functions appear in the class definition, friends are not member functions.

**Software Engineering Observation 10.9**

Member access notions of private, protected and public are not relevant to friend declarations, so friend declarations can be placed anywhere in a class definition.

**Good Programming Practice 10.1**

Place all friendship declarations first inside the class definition’s body and do not precede them with any access specifier.

Friendship is granted, not taken—i.e., for class B to be a friend of class A, class A must explicitly declare that class B is its friend. Also, the friendship relation is neither symmetric nor transitive; i.e., if class A is a friend of class B, and class B is a friend of class C, you cannot infer that class B is a friend of class A (again, friendship is not symmetric), that class C is a friend of class B (also because friendship is not symmetric), or that class A is a friend of class C (friendship is not transitive).

**Software Engineering Observation 10.10**

Some people in the OOP community feel that “friendship” corrupts information hiding and weakens the value of the object-oriented design approach. In this text, we identify several examples of the responsible use of friendship.

# Modifying a Class’s private Data with a Friend Function

Figure 10.15 is a mechanical example in which we define friend function setX to set the private data member x of class Count. The friend declaration (line 9) appears first (by convention) in the class definition, even before public member functions are declared. Again, this friend declaration can appear anywhere in the class.

```
```cpp
// Fig. 10.15: fig10_15.cpp
// Friends can access private members of a class.
#include <iostream>
using namespace std;

// Count class definition
class Count
{
    friend void setX( Count &, int ); // friend declaration
public:
    // constructor
    Count()
        : x( 0 ) // initialize x to 0
    {
        // empty body
    } // end constructor Count
```

```

**Fig. 10.15**  |  Friends can access private members of a class. (Part 1 of 2.)