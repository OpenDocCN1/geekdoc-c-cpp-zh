# // QUIZ ANSWERS

1 a False. Dynamic memory is also known as the heap or the free store; the stack is used to refer to static memory.

b False. Those "normal" declarations are for variables you know exist at compile time. They are allocated in static memory; dynamic memory is allocated when you use new to set aside memory during a program’s execution that was not necessarily known ahead of time.

c True. The vector class is one example. It is performing dynamic memory allocation to grow as needed when additional items are pushed onto the back of the vector.

d False. Dynamic memory allocation has the potential for creating numerous bugs, security flaws, and general program instability. It is better to use static memory when feasible and to use dynamic memory allocation when you need to. An example of when you might need to is when you are dealing with an indeterminate amount of data.

2 a No. This is not a good reason on its own. Whether variables are private or public does not really matter as far as whether a destructor is needed.

b Yes. This is typically a main reason a destructor is used. A destructor will typically free the memory that was dynamically allocated for that object so that it does not stay allocated when the object is deleted.

c Yes. This is a reason to implement a destructor. If other objects are pointing to this object, then when it is deleted, they could have a bad pointer. The destructor might include code that tells those objects that this one is being deleted.

```
testclass* p;
```

The * indicates that the new variable will be a pointer to something of that type.

b Here are 2 options:

```
p = new testclass;
OR
p = new testclass();
```

In either case, the default constructor is called.

```
p = new testclass(5);
```

By giving arguments when allocating the object, the corresponding constructor is called for that object.

```
p = new testclass[5];
```

This allocates an array of 5 objects, each initialized with the default constructor.

e Here are 3 equivalent options:

```
p->print();
(*p).print();
p[0].print();
```

In each case, the pointer is dereferenced to get the object it is pointing to and then the function is called for that object.