# Programming Tip: Initializers versus methods for constructors

Chapter 3 suggested that you use initializers instead of assignment statements in constructors to initialize the values of a class's data members. That is still good advice, and initials clearly show the initialization. However, if you write methods to alter the values of the data members, you have the opportunity to ensure that the values are assigned. Doing so is especially important when these values are supplied by the client. In some cases, you can call the methods to initialize the data members. Thus, we have the following advice when you initialize the values of data members in constructors:

+   * Use an initializer if the value of the data member has restrictions.
* Use a method if the value of the data member needs validation.

Note that if you do not publish a public set method for a particular data member, you can either define a private one for the constructor to call or have the constructor perform its own validation.

Validate any data client gives you

# 7.3 Implementations That Use Exceptions

Our specifications of the ADT stack appear to handle all eventualities. If you try to add an item to a full stack, the method push returns false. If you try to remove an entry from an empty stack, the method pop returns false. What happens when try to look at the top of an empty stack? The method expects you to not do this, as stated in its precondition. Our implementations, deal with the misuse of this method by beginning its definition with the statement

```
assert(isEmpty());
```

If the stack is empty, assert will issue an error message and halt execution.
Instead of using assert, peak could throw an exception if its precondition is violated—that is, if it is called when the stack is empty. Let's define the class PreconditionViolatedException that peak can use. Listings 7-5 and 7-6 show this class.

# LISTING 7-5 header file for the class PreconditionViolatedException

```
/* PreconditionViolatedException.h */
#ifndef PRECONDITION_VIOLATED_EXCEPT
#define PRECONDITION_VIOLATED_EXCEPT

#include <stdexcept>
#include <string>

using namespace std;

class PreconditionViolatedException: public logic_error
{
public:
    PreconditionViolatedException(const string& message = "");
};\ // end PreconditionViolatedException
#endif
```