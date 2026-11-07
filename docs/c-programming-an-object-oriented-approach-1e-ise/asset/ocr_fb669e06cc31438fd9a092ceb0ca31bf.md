The main difference between the definition of a constructor and definition of other member functions is that a constructor can have an initialization list after the header to initialize the data members. The initialization list is put after the header and before the body of the constructor and it starts with a colon. In our *Circle* class, we have only one data member to initialize. If we need to initialize more than one data member, the initialization of each data member must be separated by a comma from other data members. In general, the initialization list has the following format:

```
: dataMember (parameter), ... , dataMember (parameter)
```

We can think of each initialization as an assignment statement that assigns the parameter to the data member, such as `dataMember = parameter`. There is no terminator for the initialization list. The next line is the body of the constructor. The *dataMember* name must be the same as the one defined in the declaration of the data member, but the name of each parameter is determined by the programmer.

Another important point is that a constant data member of an object must be initialized when the object is created. As we have seen in previous chapters, we cannot change a constant entity after it has been declared, but C++ allows us to initialize it in the initialization section of a constructor.

Sometimes, however, we must use the body of the constructor to initialize complex data members (through assignments) that cannot be simply initialized in the initialization list. The body of a constructor can also be used for additional processing, such as validating a parameter, opening files if needed, or even printing a message to verify that the constructor was called.

# 7.3.2 Destructors

Like a constructor, a destructor has two special characteristics. First, the name of the destructor is the name of the class preceded by a tilde symbol (~), but the tilde is added to the first name, not the last name (the last name is the same for all member functions). Second, like a constructor, a destructor cannot have a return value (not even *void*) because it returns nothing. A destructor is guaranteed to be automatically called and executed by the system when the object instantiated from the class goes out of scope. In other words, if we have instantiated five objects from the class, the destructor is automatically called five times to guarantee that all objects are cleaned up. Cleanup is most important if the constructed has released resources such as files. After the program is terminated, the allocated memory is recycled. A destructor can take no arguments, which means it cannot be overloaded.

> A destructor is a special-purpose member function with no parameter and is designed to clean up and recycle an object.

# Destructor Declaration

The following shows the declaration of the destructor in the class definition.

```
class Circle
{
    ...
    public:
        ...
        ~Circle();                 // Destructor
}
```