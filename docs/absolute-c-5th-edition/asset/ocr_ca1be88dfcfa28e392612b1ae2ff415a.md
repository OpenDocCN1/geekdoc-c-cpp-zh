# Chapter Summary 683

changed, then its entry points to the definition for that function that was given in the parent class (or other ancestor class if need). If another virtual function had a new definition in the class, the pointer for that member function points to that definition. (Remember that the property of being a virtual function is inherited, once a class has a virtual function table, all its descendant classes have a virtual table.)

Whenever an object of class with one or more virtual functions is created, a pointer is added to the description of the object that is stored in memory. This pointer points to the class's virtual function table. When you make a call to a member function using a pointer (ep, another one) to the object, the run-time system uses the virtual function table to decide which definition of a member function to use; it does not use the type of pointer.

Of course, this happens automatically, so you do not worry about it. A compiler writer is free to implement virtual functions in some other way as long as it works correctly (although it never actually is implemented in a different way).

![](bbox=[0.048, 0.406, 0.172, 0.431])

# Self-Test Exercise

+   8. Why is the following illegal?

```
Pet vpet;
Dog vdog; //Dog is a derived class with base class Pet.
...
vdog  = static_cast(vpet); //ILLEGAL!
```

# Chapter Summary

+   * Late binding means that the decision of which version of a member function is appropriate at run time. In C++, member functions that use late binding are called virtual functions. Polymorphism is another word for late binding.

+   * A pure virtual function is a member function that has no definition. It is indicated by the word virtual and the notation =\0 in the member function declaration. A class with one or more virtual functions is called an abstract class.

+   * An abstract class is a type and can be used as a base class to derive other classes. However, you cannot create an object of an abstract class type (unless it is an object of some derived class).

+   * You can assign an object of a derived class to a variable of its base class (or any ancestor class), but the member variables that are not in the base class are lost. This is known as the slicing problem.