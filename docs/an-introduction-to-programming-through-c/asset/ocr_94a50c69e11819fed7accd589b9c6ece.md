```
mTurtleI(double x, double y) : Turtle(x,y), distance() {}
```

With this constructor, the metered turtle would be created at position (x,y) on the screen, and the new member distance would be initialized to 0 using the initialization list. The body of the constructor would then be left empty.

# 23.2.3 Destructors

As before suppose we have a class B which inherits from class A. Then the destructor for class B should be used to destroy the new data members introduced in B that were not present in A. The data members inherited from A? These would be destroyed by an implicit call that would get made to the destructor of A at the end of the execution of the call to the destructor of B. You should not explicitly make a call to the destructor of A from inside the destructor of B!

The general rule is: destruction happens automatically, in reverse order of creation. In the exercises you will experiment with code which will illustrate these ideas.

# 23.2.4 Basic operations on subclass objects

A subclass is a class, so all operations allowed on objects of classes are allowed on objects of subclasses, and work similarly. For example, objects can be copied, passed to functions, and so on, as discussed in Chapter 15.

# 23.2.5 The type of a subclass object

We have said that a class is a type, i.e. an object of class A has type A. Suppose B is a subclass of class A. Then a key idea in inheritance is: objects of class B can be considered to have type B as well as type A. This idea turns out to be quite useful.

The following analogy might be useful to understand this. Consider the category of flowers, in which we have subcategories such as roses, lotuses and so on. So if someone has demanded flowers, we can give roses. In other words, a specific rose object is useful as a rose as well as as a flower.

# 23.2.6 Assignments mixing superclass and subclass objects

If an object can be considered to be of the type of its superclass, we should allow an object of a subclass to be assigned to variable of the superclass. This is indeed possible. Note however that the subclass might have some additional data members. In such a case, the additional members are dropped, or sliced off, during the assignment.

You can also assign the address of a subclass object into a pointer variable of the superclass.

Figure 23.3 shows some examples. First we have tha assignment a = b. Since b has an extra attribute y, during the assignment this will be sliced off, and only the attribute x will get copied. Thus the first print statement will print 2, the value that got copied.

Next we have aptr = &b, which stores the address of the class B object b into the pointer variable aptr of type A*. As we said, this is allowed, since A is a superclass of B. The next