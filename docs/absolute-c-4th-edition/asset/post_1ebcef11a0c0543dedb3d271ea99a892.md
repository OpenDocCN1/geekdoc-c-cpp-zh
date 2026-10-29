
When this assignment is executed, the first statement executed is

`delete [] a;`

But the calling object is myList, so this means

`delete [] myList.a;`

The pointer myList.a is then undefined. The assignment operator has corrupted the object myList. This problem cannot happen with the definition of the overloaded assignment operator we gave in Display 10.11.

## SHALLOW COPY AND DEEP COPY

When defining an overloaded assignment operator or a copy constructor, if your code simply copies the contents of member variables from one object to the other that is known as a shallow copy. The default assignment operator and the default copy constructor perform shallow copies. If there are no pointers or dynamically allocated data involved, this works fine. If some member variable names a dynamic array or points to some other dynamic structure, then you normally do not want a shallow copy. Instead, you want to create a copy of what each member variable is pointing to, so that you get a separate but identical copy, as illustrated in Display 10.10. This is called a deep copy and is what we normally do when overloading the assignment operator or defining a copy constructor.

## DESTRUCTORS

Dynamically allocated variables have one problem: They do not go away unless your program makes a suitable call to delete. Even if the dynamic variable was created using a local pointer variable and the local pointer variable goes away at the end of a function call, the dynamic variable will remain unless there is a call to delete. If you do not eliminate dynamic variables with calls to delete, the dynamic variables will continue to occupy memory space, which may cause your program to abort by using up all the memory in the freestore manager. Moreover, if the dynamic variable is embedded in the implementation details of a class, the programmer who uses the class may not know about the dynamic variable and cannot be expected to perform the calls to delete. In fact, since the data members are normally private members, the programmer normally cannot access the needed pointer variables and so cannot call delete with these pointer variables. To handle this problem, C++ has a special kind of member function called a destructor.

A destructor is a member function that is called automatically when an object of the class passes out of scope. If your program contains a local variable that names an object from a class with a destructor, then when the function call ends, the destructor will be called automatically. If the destructor is defined correctly, the destructor will call delete to eliminate all the dynamically allocated variables created by the object. This may be done with a single call to delete or it may require several calls to delete. You may also want your destructor to perform some other clean-up details as well, but returning memory to the freestore manager for reuse is the main job of the destructor.

The member function ~PFArrayD is the destructor for the class PFArrayD shown in Display 10.10. Like a constructor, a destructor always has the same name as the class of which it is a member, but the destructor has the tilde symbol, ~, at the beginning of its name (so you can tell that it is a destructor and not a constructor). Like a constructor, a destructor has no type for the value returned, not even the type void. A destructor has no parameters. Thus, a class can have only one destructor; you cannot overload the destructor for a class. Otherwise, a destructor is defined just like any other member function.

Notice the definition of the destructor ~PFArrayD given in Display 10.11. ~PFArrayD calls delete to eliminate the dynamically allocated array pointed to by the member pointer variable a. Look again at the function testPFArrayD in the sample program shown in Display 10.12. The local variable temp contains a dynamic array pointed to by the member variable temp.a. If this class did not have a destructor, then after the call to testPFArrayD ended, this dynamic array would still be occupying memory, even though the dynamic array is useless to the program. Moreover, every iteration of the do-while loop would produce another useless dynamic array to clutter up memory. If the loop is iterated enough times, the function calls could consume all the memory in the freestore manager and your program would then end abnormally.

### DESTRUCTOR

The destructor of a class is a member function of a class that is called automatically when an object of the class goes out of scope. Among other things, this means that if an object of the class type is a local variable for a function, then the destructor is automatically called as the last action before the function call ends. Destructors are used to eliminate any dynamically allocated variables that have been created by the object so that the memory occupied by these dynamic variables is returned to the freestore manager for reuse. Destructors may perform other clean-up tasks as well. The name of a destructor must consist of the tilde symbol, ~, followed by the name of the class.

## COPY CONSTRUCTORS

A copy constructor is a constructor that has one parameter that is of the same type as the class. The one parameter must be a call-by-reference parameter, and normally the parameter is preceded by the const parameter modifier, so it is a constant parameter. In all other respects a copy constructor is defined in the same way as any other constructor and can be used just like other constructors. For example, a program that uses the class PFArrayD defined in Display 10.10 might contain the following:

```
PFArrayD b(20);

for (int i = 0; i < 20; i++)
    b.addElement(i);

PFArrayD temp(b);//Initialized by the copy constructor
```

The object b is initialized with the constructor that has a parameter of type int. Similarly, the object temp is initialized by the constructor that has one argument of type const PFArrayD&. When used in this way a copy constructor is being used just like any other constructor.

A copy constructor should be defined so that the object being initialized becomes a complete, independent copy of its argument. So, in the declaration

```
PFArrayD temp(b);
```

the member variable temp.a should not be simply set to the same value as b.a; that would produce two pointers pointing to the same dynamic array. The definition of the copy constructor is shown in Display 10.11. Note that in the definition of the copy constructor, a new dynamic array is created and the contents of one dynamic array are copied to the other dynamic array. Thus, in the above declaration, temp is initialized so that its array member variable is different from the array member variable of b. The two array member variables, temp.a and b.a, contain the same values of type double, but if a change is made to one of these array member variables, it has no effect on the other array member variable. Thus, any change that is made to temp will have no effect on b.

As you have seen, a copy constructor can be used just like any other constructor. A copy constructor is also called automatically in certain other situations. Roughly speaking, whenever C++ needs to make a copy of an object, it automatically calls the copy constructor. In particular, the copy constructor is called automatically in three circumstances:

- 1. When a class object is being declared and is initialized by another object of the same type given in parentheses. (This is the case of using the copy constructor like any other constructor.)
- 2. When a function returns a value of the class type.
- 3. Whenever an argument of the class type is "plugged in" for a call-by-value parameter. In this case, the copy constructor defines what is meant by "plugging in."

If you do not define a copy constructor for a class, C++ will automatically generate a copy constructor for you. However, this default copy constructor simply copies the contents of member variables and does not work correctly for classes with pointers or dynamic data in their member variables. Thus, if your class member variables involve pointers, dynamic arrays, or other dynamic data, you should define a copy constructor for the class.

To see why you need a copy constructor, let's see what would happen if we did not define a copy constructor for the class PFArrayD. Suppose we did not include the copy
