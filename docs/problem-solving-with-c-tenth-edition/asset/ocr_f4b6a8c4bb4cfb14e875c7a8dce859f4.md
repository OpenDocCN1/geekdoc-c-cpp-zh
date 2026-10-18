Derived, the destructor for the class Derived is called (and it in turn calls the destructor for the class Base). If the destructor in the class Base had not been declared as virtual, then only the destructor in the class Base would be called.

Another point to keep in mind is that when a destructor is marked as virtual, then all destructors of derived classes are automatically virtual (whether or not they are marked virtual). Again, this behavior is as if all destructors had the same name (even though they do not).

Now we are ready to explain why all destructors should be virtual. Suppose the class Base has a member variable pB of a pointer type, the constructor for the class Base creates a dynamic variable pointed to by pB, and the destructor for the class Base deletes the dynamic variable pointed to by pB. And suppose the destructor for the class Base is not marked virtual. Also suppose that the class Derived (which is derived from Base) has a member variable pD of a pointer type, the constructor for the class Derived creates a dynamic variable pointed to by pD, and the destructor for the class Derived deletes the dynamic variable pointed to by pD. Consider the following code:

```
Base *pBase = new Derived;
...
delete pBase;
```

Since the destructor in the base class is not marked virtual, only the destructor for the class Base will be invoked. This will return to the freestore the memory for the dynamic variable pointed to by pB, but the memory for the dynamic variable pointed to by pD will never be returned to the freestore (until the program ends).

On the other hand, if the destructor for the base class Base were marked virtual, then when delete is applied to pBase, the destructor for the class Derived would be invoked (since the object pointed to is of type Derived). The destructor for the class Derive would delete the dynamic variable pointed to by pD and then automatically invoke the destructor for the base class Base, and that would delete the dynamic variable pointed to by pB. So, with the base class destructor marked as virtual, all the memory is returned to the freestore. To prepare for eventualities such as these, it is best to always mark destructors as virtual.

# SELF-TEST EXERCISES

+   12. Why can’t we assign a base class object to a derived class variable?

+   13. What is the problem with the (legal) assignment of a derived class object to a base class variable?

+   14. Suppose the base class and the derived class each have a member function with the same signature. When you have a pointer to a base class object