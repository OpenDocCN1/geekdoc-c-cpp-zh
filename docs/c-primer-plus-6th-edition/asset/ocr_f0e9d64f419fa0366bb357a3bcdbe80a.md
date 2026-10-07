# Why TwoKinds of Binding and Why Static is the Default

If dynamic binding allows you to redefine class methods but static binding makes a partial botch of it, why static binding at all? There are two reasons: efficiency and a conceptual model.

First, let's consider efficiency. For a program to be able to make a runtime decision, it has some way to keep track of what sort of object a base-class pointer or reference refers to, and that entails some extra overhead. (You'll see one method of dynamic binding later). If, for example, you design a class that won't be used as a base class for inheritance, or if you have a derived class, such as the RatedPlayer example, that does not redefine methods, then you won't need dynamic binding. Similarly, if you do, in these cases it makes sense to use static binding and gain a little efficiency. The fact that static binding is more efficient is the default choice for C++. Stroustrup says one of the principles of C++ is that you shouldn't have to pay (in memory usage or processing time) for functions that you don't use. You should go to virtual functions only if the program design needs them.

Next, consider the conceptual model. When you design a class, you may have member functions that you don't want redefined in derived classes. For example, the Balance() function, which returns the account balance, seems like a function that shouldn't be redefined. By making it nonvirtual, you accomplish two things. First, make it efficient. Second, you announce that it is your intention that this function not be redefined. That suggests reserving the virtual label just for methods you expect to be redefined.

> Tip
If a method in a base class will be redefined in a derived class, you should not be redefined, you should make it nonvirtual.

Of course, when you design a class, it's not obvious into which category a method falls. Many aspects of real life, class design is not a linear process.

# Virtual Functions Work

C++ specifies how virtual functions should behave, but it leaves the implementation up to the compiler writer. Use virtual functions, but seeing how it is done may help you understand the concepts better, so let's take a look.

The usual way compilers handle virtual functions is to add a hidden member to each object. The hidden member holds a pointer to an array of addresses. Such an array is termed a virtual function table (vtable). The vtable holds the addresses of the virtual functions declared for objects of that class. For example, an object of a base class contains a pointer to a table of addresses of all the virtual functions for that. An object of a derived class contains a pointer to a separate table of addresses. If the derived class provides a new definition of a virtual function, the vtable holds the address of the new function.