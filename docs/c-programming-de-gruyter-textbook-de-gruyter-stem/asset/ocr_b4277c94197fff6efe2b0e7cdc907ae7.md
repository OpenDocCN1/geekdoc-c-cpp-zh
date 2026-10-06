# 4.3 Constructor and Destructor — 131

can use white paper to cover the unneeded part before the copying. There are many other situations, such as when we want to copy with zooming in or out, etc. Things are similar in object copying in programs, where we can copy an object according to our needs. Readers can try to modify the above example code to make the copy constructor construct a new point with a certain amount offset from the old point. Besides, when some of the data members are of pointer types, default copy constructor can only do shallow copying, which causes security problems. To achieve the correct copy, i.e., deep copy, we must write our own copy constructor. Details about pointer types and issues of deep copy will introduced in Chapter 6. Examples in Chapter 9 will show more about deep copy.

# 4.3.3 Class Destructor

Besides is a good start, we also need a good finish. Programming also needs to consider the round-off work. In C++, when an object disappears, we often need to take care of the mop-up.

Will an object disappear? Sure! Like every thing in the world, objects in programs have their own lifetime. We already know that an object is created when it is defined, and when the object disappears involves the issues of the object's lifetime, which will be discussed in Chapter 5. Here we only consider one situation: if a local object is defined inside a function, then it will disappear when the function terminates.

What should be done when an object is going to disappear? The most classical situation is: when constructing an object, some resources are allocated by the constructor, such as dynamically allocating memory space. When the object disappears, these resources have to be released. This is reflected in Examples 7.10 in Chapter 7, in some examples in Chapter 9, and is detailed in Section 7.74"Running Result and Analysis". Dynamic memory allocation is detailed in Chapter 6. In this chapter, we just make a simple introduction of using destructors to do the round-off work.

Basically, a destructor does almost exactly the opposite of what constructor does. A destructor does some round-off work before the object disappears. A destructor is called automatically when the lifetime of the object ends. After calling the destructor, the object disappears and the corresponding memory space is released.

Like a constructor, a destructor is often a public member function. Its name is composed of the class name with the prefix '~'. The destructor has no return value. Differently from constructors, destructors do not accept any parameter, while it can be a virtual function (Chapter 8 will introduce virtual functions). If not declared explicitly, the system will also generate a default destructor, which does nothing.

For example, we add an empty inline destructor to class Clock, which has the same function as the default destructor that the system generates.