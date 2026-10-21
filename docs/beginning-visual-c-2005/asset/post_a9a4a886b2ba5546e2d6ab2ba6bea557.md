
## Overloading the Assignment Operator

If you don’t provide an overloaded assignment operator function for your class, the compiler provides a default. The default version simply provides a member-by-member copying process, similar to that of the default copy constructor; however, don’t confuse the default copy constructor with the default assignment operator. The default copy constructor is called by a declaration of a class object that’s initialized with an existing object of the same class or by passing an object to a function by value. The default assignment operator, on the other hand, is called when the left side and the right side of an assignment statement are objects of the same class type.

For the CBox class, the default assignment operator works with no problem, but for any class that has space for members allocated dynamically, you need to look carefully at the requirements of the class in question. There may be considerable potential for chaos in your program if you leave the assignment operator out under these circumstances.

For a moment, return to the CMessage class that you used when I was talking about copy constructors. Remember it had a member, pmessage, that was a pointer to a string. Now consider the effect that the default assignment operator could have. Suppose you had two instances of the class, motto1 and motto2. You could try setting the members of motto2 equal to the members of motto1 using the default assignment operator, as follows:

```
motto2 = motto1;              // Use default assignment operator
```

The effect of using the default assignment operator for this class is essentially the same as using the default copy constructor: disaster will result! Because each object has a pointer to the same string, if the string is changed for one object, it’s changed for both. There’s also the problem that when one of the instances of the class is destroyed, its destructor frees the memory used for the string and the other object is left with a pointer to memory that may now be used for something else.

What you need the assignment operator to do is to copy the text to a memory area owned by the destination object.

### Fixing the Problem

You can fix this with your own assignment operator function, which we will assume is defined within the class definition:

```
// Overloaded assignment operator for CMessage objects
CMessage& operator=(const CMessage& aMess)
{
    // Release memory for 1st operand
    delete[] pmessage;
    pmessage = new char[strlen(aMess.pmessage) + 1];

    // Copy 2nd operand string to 1st
    strcpy(this->pmessage, aMess.pmessage);

    // Return a reference to 1st operand
    return *this;
}
```

An assignment might seem very simple, but a couple of subtleties need further investigation. Note that you return a *reference* from the assignment operator function. It may not be immediately apparent why this is so (after all, the function does complete the assignment operation entirely, and the object on the right of the assignment is copied to that on the left). Superficially this would suggest that you don’t need to return anything, but you need to consider how the operator might be used in a little more depth.

There’s a possibility that you might need to use the result of an assignment operation on the right side of an expression. Consider a statement such as this:

```
motto1 = motto2 = motto3;
```

Because the assignment operator is right-associative, the assignment of motto3 to motto2 is carried out first, so this translates into the following statement:

```
motto1 = (motto2.operator=(motto3));
```

The result of the operator function call here is on the right of the equals sign, so the statement finally becomes this:

```
motto1.operator=(motto2.operator=(motto3));
```

If this is to work, you certainly have to return something. The call of the operator=() function between the parentheses must return an object that can be used as an argument to the other operator=() function call. In this case a return type of either CMessage or CMessage& would do it, so a reference is not mandatory in this situation, but you must at least return a CMessage object.

However, consider the following example:

```
(motto1 = motto2) = motto3;
```

This is perfectly legitimate code (the parentheses serve to make sure the leftmost assignment is carried out first). This translates into the following statement:

```
(motto1.operator=(motto2)) = motto3;
```

When you express the remaining assignment operation as the explicit overloaded function call, this ultimately becomes:

```
(motto1.operator=(motto2)).operator=(motto3);
```

Now you have a situation where the object returned from the operator=() function is used to call the operator=() function. If the return type is just CMessage, this is not legal, because a temporary copy of the original object is actually returned, and the compiler does not allow a member function call using a temporary object. In other words, the return value when the return type is CMessage is not an lvalue. The only way to ensure this sort of thing compiles and works correctly is to return a reference, which is an lvalue, so the only possible return type if you want to allow fully flexible use of the assignment operator with your class objects is CMessage&.

Note that the native C++ language does not enforce any restrictions on the accepted parameter or return types for the assignment operator, but it makes sense to declare the operator in the way I have just described if you want your assignment operator functions to support normal C++ usage of assignment.

The second subtlety you need to keep in mind is that each object already has memory for a string allocated, so the first thing that the operator function has to do is to delete the memory allocated to the first object and reallocate sufficient memory to accommodate the string belonging to the second object. After this is done, the string from the second object can be copied to the new memory now owned by the first.

There’s still a defect in this operator function. What if you were to write the following statement?

```
motto1 = motto1;
```

Obviously, you wouldn’t do anything as stupid as this directly, but it could easily be hidden behind a pointer, for instance, as in the following statement.

```
motto1 = *pMess;
```

If the pointer pMess points to motto1, you essentially have the preceding assignment statement. In this case, the operator function as it stands would delete the memory for motto1, allocate some more memory based on the length of the string that has already been deleted and try to copy the old memory which, by then, could well have been corrupted. You can fix this with a check for identical left and right operands at the beginning of the function, so now the definition of the operator=() function would become this:

```
// Overloaded assignment operator for CMessage objects
CMessage& operator=(const CMessage& aMess)
{
    if (this == &aMess)           // Check addresses, if equal
        return *this;             // return the 1st operand

    // Release memory for 1st operand
    delete[] pmessage;
    pmessage = new char[strlen(aMess.pmessage) + 1];

    // Copy 2nd operand string to 1st
    strcpy(this->pmessage, aMess.pmessage);

    // Return a reference to 1st operand
    return *this;
}
```

This code assumes that the function definition appears within the class definition.

### Try It Out Overloading the Assignment Operator

Let’s put this together in a working example. We’ll add a function, called Reset(), to the class at the same time. This just resets the message to a string of asterisks.

```
// Ex8_05.cpp
// Overloaded copy operator perfection
#include <iostream>
#include <cstring>
using std::cout;
using std::endl;

class CMessage

int main()
{
    CMessage motto1("The devil takes care of his own");
    CMessage motto2;

    cout << "motto2 contains - ";
    motto2.ShowIt();
    cout << endl;

    motto2 = motto1;                    // Use new assignment operator

    cout << "motto2 contains - ";
    motto2.ShowIt();
    cout << endl;

    motto1.Reset();                     // Setting motto1 to * doesn't
                                        // affect motto2

    cout << "motto1 now contains - ";
    motto1.ShowIt();
    cout << endl;

    cout << "motto2 still contains - ";
    motto2.ShowIt();
    cout << endl;

    return 0;
}
```

You can see from the output of this program that everything works exactly as required, with no linking between the messages of the two objects, except where you explicitly set them equal:

```
motto2 contains -
Default message
motto2 contains -
The devil takes care of his own
motto1 now contains -
********************************
motto2 still contains -
The devil takes care of his own
Destructor called.
Destructor called.
```

So let’s have another golden rule out of all of this:

> *Always implement an assignment operator if you allocate space dynamically for a data member of a class.*

Having implemented the assignment operator, what happens with operations such as `+=`? Well, they don’t work unless you implement them. For each form of `op=` that you want to use with your class objects, you need to write another operator function.
