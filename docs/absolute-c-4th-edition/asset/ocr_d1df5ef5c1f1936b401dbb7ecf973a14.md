When this assignment is executed, the first statement executed is

`delete [] a;`

But the calling object is myList, so this means

`delete [] myList.a;`

The pointer myList.a is then undefined. The assignment operator has corrupted the object myList. This problem cannot happen with the definition of the overloaded assignment operator we gave in Display 10.11.

# SHALLOW COPY AND DEEP COPY

When defining an overloaded assignment operator or a copy constructor, if your code simply copies the contents of member variables from one object to the other that is known as a shallow copy. The default assignment operator and the default copy constructor perform shallow copies. If there are no pointers or dynamically allocated data involved, this works fine. If some member variable names a dynamic array or points to some other dynamic structure, then you normally do not want a shallow copy. Instead, you want to create a copy of what each member variable is pointing to, so that you get a separate but identical copy, as illustrated in Display 10.10. This is called a deep copy and is what we normally do when overloading the assignment operator or defining a copy constructor.

# DESTRUCTORS

Dynamically allocated variables have one problem: They do not go away unless your program makes a suitable call to delete. Even if the dynamic variable was created using a local pointer variable and the local pointer variable goes away at the end of a function call, the dynamic variable will remain unless there is a call to delete. If you do not eliminate dynamic variables with calls to delete, the dynamic variables will continue to occupy memory space, which may cause your program to abort by using up all the memory in the freestore manager. Moreover, if the dynamic variable is embedded in the implementation details of a class, the programmer who uses the class may not know about the dynamic variable and cannot be expected to perform the calls to delete. In fact, since the data members are normally private members, the programmer normally cannot access the needed pointer variables and so cannot call delete with these pointer variables. To handle this problem, C++ has a special kind of member function called a destructor.

A destructor is a member function that is called automatically when an object of the class passes out of scope. If your program contains a local variable that names an