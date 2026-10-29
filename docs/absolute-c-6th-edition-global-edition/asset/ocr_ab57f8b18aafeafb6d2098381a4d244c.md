program shown in Display 10.12. The local variable temp contains a dynamic array pointed to by the member variable temp.a. If this class did not have a destructor, then after the call to testPFArrayD ended, this dynamic array would still be occupying memory, even though the dynamic array is useless to the program. Moreover, every iteration of the do-while loop would produce another useless dynamic array to clutter up memory. If the loop is iterated enough times, the function calls could consume all the memory in the freestore manager and your program would then end abnormally.

# Destructor

The destructor of a class is a member function of a class that is called automatically when an object of the class goes out of scope. Among other things, this means that if an object of the class type is a local variable for a function, then the destructor is automatically called as the last action before the function call ends. Destructors are used to eliminate any dynamically allocated variables that have been created by the object so that the memory occupied by these dynamic variables is returned to the freestore manager for reuse. Destructors may perform other clean-up tasks as well. The name of a destructor must consist of the tilde symbol, ~, followed by the name of the class.

# Copy Constructors

copy constructor

A copy constructor is a constructor that has one parameter that is of the same type as the class. The one parameter must be a call-by-reference parameter, and normally the parameter is preceded by the const parameter modifier, so it is a constant parameter. In all other respects a copy constructor is defined in the same way as any other constructor and can be used just like other constructors. For example, a program that uses the class PFArrayD defined in Display 10.10 might contain the following:

```
PFArrayD b(20);
for (int i = 0; i < 20; i++)
    b.addElement(i);
PFArrayD temp(b); // Initialized by the copy constructor
```

The object b is initialized with the constructor that has a parameter of type int. Similarly, the object temp is initialized by the constructor that has one argument of type const PFArrayD&. When used in this way a copy constructor is being used just like any other constructor.

A copy constructor should be defined so that the object being initialized becomes a complete, independent copy of its argument. So, in the declaration
PFArrayD temp(b);

the member variable temp.a should not be simply set to the same value as b.a; that would produce two pointers pointing to the same dynamic array. The definition of the copy constructor is shown in Display 10.11. Note that in the definition of the copy constructor, a new dynamic array is created and the contents of one dynamic