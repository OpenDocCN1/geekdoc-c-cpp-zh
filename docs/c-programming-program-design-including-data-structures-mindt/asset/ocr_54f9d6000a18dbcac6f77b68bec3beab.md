The statement in Line 4 outputs the arrival time of an employee in the form **hr:min:sec**.

To keep track of the departure time of each employee, you can use the array **departureTimeEmp**.

Similarly, you can use arrays to manage a list of names or other objects.

![](bbox=[0.182, 0.204, 0.232, 0.253])

> > Before leaving our discussion of arrays of class objects, we would like to point out the following: The beginning of this section stated that if you declare an array of class objects and the class has constructor(s), then the class should have the default constructor. The compiler uses the default constructor to initialize the array of objects. If the array size is large, then it is impractical to specify a different constructor with parameters for each object. For a small-sized array, we can manage to specify a different constructor with parameters.

> > For example, the following statement declares `clocks` to be an array of two components. The member variables of the first component are initialized to 8, 35, and 42, respectively. The member variables of the second component are initialized to 6, 52, and 39, respectively.

```
clockType clocks[2] = {clockType(8, 35, 42),
                    clockType(6, 52, 39)};
```

> > In fact, the expression `clockType(8, 35, 42)` creates an anonymous object of the class `clockType`, initializes its member variables to 8, 35, and 42, respectively; and then uses a member-wise copy to initialize the object `clock[0]`.

> > Consider the following statement, which creates the object `myClock` and initializes its member variables to 10, 45, and 38, respectively. This is how we have been creating and initializing objects. In fact, the statement:

```
clockType myClock(10, 45, 38);
```

> > is equivalent to the statement:

```
clockType myClock = clockType(10, 45, 38);
```

> > However, the first statement is more efficient. It does not first require that an anonymous object be created and then member-wise copied in order to initialize `myClock`.

> > The main point that we are stressing here, and that we discussed in the preceding section, is the following: To avoid any pitfalls, if a class has constructor(s), it should also have the default constructor.

# ## Destructors

Like constructors, destructors are also functions. Moreover, like constructors, a destructor does not have a type. That is, it is neither a value-returning function nor a void function. However, a class can have only one destructor, and the destructor has no parameters. The name of a destructor is the *tilde* character (`~`), followed by the name of the class. For example, the name of the destructor for the class `clockType` is:

```
~clockType();
```