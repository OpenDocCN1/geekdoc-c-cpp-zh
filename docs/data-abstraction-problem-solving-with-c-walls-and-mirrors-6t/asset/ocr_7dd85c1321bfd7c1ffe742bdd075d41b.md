# Programming Tip: Initializers versus set methods for constructors

Chapter 3 suggested that you use initializers instead of assignment statements in constructors to initialize the values of a class's data members. That is still good advice, and initializers clearly show the initialization. However, if you write set methods to alter the values of the data members, you have the opportunity to ensure that the values assigned are valid. Doing so is especially important when those values are supplied by the client. In such cases, constructors can call the set methods to initialize the data members. Thus, we have the following advice when you initialize the values of data members in constructors:

+   - Use an initializer if the value of the data member has no restrictions.
+   - Use a set method if the value of the data member needs validation.

Note that even if you do not want a public set method for a particular data member, you can either define a private one for the constructor to call or have the constructor perform its own validation.

Validate any data a client gives you

# 7.3 Implementations That Use Exceptions

Our specifications of the ADT stack appear to handle all eventualities. If you try to add an item to a full stack, the method push returns false. If you try to remove an entry from an empty stack, the method pop returns false. What happens when you try to look at the top of an empty stack? The method peek expects that you will not do this, as stated in its precondition. Our implementation, however, deal with the misuse of this method by beginning its definition with the statement assert(!isEmpty());

If the stack is empty, assert will issue an error message and halt execution.

Instead of using assert, peek could throw an exception if its precondition is violated—that is, if it is called when the stack is empty. Let's define the class PrecondViolatedExcep that peek can use. Listings 7-5 and 7-6 show this class.

```
LISTING 7-5 The header file for the class PrecondViolatedExcep
/** @file PrecondViolatedExcep.h */
#ifndef _PRECOND_VIOLATED_EXCEP
#define _PRECOND_VIOLATED_EXCEP

#include <stdexcept>
#include <string>

using namespace std;

class PrecondViolatedExcep: public logic_error
{
public:
   PrecondViolatedExcep(const string& message = "");
}; // end PrecondViolatedExcep
#endif
```