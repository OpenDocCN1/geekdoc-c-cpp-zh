```
    After attempting invalid settings:
    Universal time: 13:27:06
    Standard time: 1:27:06 PM
```

**Fig. 17.3** | Program to test class Time. (Part 2 of 2.)

# ### Calling setTime with Invalid Values

To illustrate that method setTime validates its arguments, line 30 calls setTime with invalid arguments of 99 for the hour, minute and second. This statement is placed in a try block (lines 28–31) in case setTime throws an invalid_argument exception, which it will do since the arguments are all invalid. When this occurs, the exception is caught at lines 32–35 and line 34 displays the exception's error message by calling its what member function. Lines 38–42 output the time again in both formats to confirm that setTime did not change the time when invalid arguments were supplied.

# ### Looking Ahead to Composition and Inheritance

Often, classes do not have to be created “from scratch.” Rather, they can include objects of other classes as members or they may be derived from other classes that provide attributes and behaviors the new classes can use. Such software reuse can greatly enhance productivity and simplify code maintenance. Including class objects as members of other classes is called composition (or aggregation) and is discussed in Section 17.11. Deriving new classes from existing classes is called inheritance and is discussed in Chapter 19.

# ### Object Size

People new to object-oriented programming often suppose that objects must be quite large because they contain data members and member functions. Logically, this is true—you may think of objects as containing data and functions (and our discussion has certainly encouraged this view); physically, however, this is not true.

![](bbox=[0.121, 0.625, 0.163, 0.656])

> > **Performance Tip 17.2**
> >
> > Objects contain only data, so objects are much smaller than if they also contained member functions. The compiler creates one copy (only) of the member functions separate from all objects of the class. All objects of the class share this one copy. Each object, of course, needs its own copy of the class’s data, because the data can vary among the objects. The function code is nonmodifiable and, hence, can be shared among all objects of one class.

# # 17.3 Class Scope and Accessing Class Members

A class’s data members and member functions belong to that class’s scope. Nonmember functions are defined at global namespace scope, by default.

Within a class’s scope, class members are immediately accessible by all of that class’s member functions and can be referenced by name. Outside a class’s scope, public class members are referenced through one of the handles on an object—an object name, a reference to an object or a pointer to an object. The type of the object, reference or pointer specifies the interface (e.g., the member functions) accessible to the client. [We’ll see in Section 17.13 that an implicit handle is inserted by the compiler on every reference to a data member or member function from within an object.]