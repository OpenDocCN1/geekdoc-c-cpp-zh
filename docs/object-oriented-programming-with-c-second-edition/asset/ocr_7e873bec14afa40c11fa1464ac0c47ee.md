# Object-Oriented Programming with C++

value would have to be maintained for this data in all objects. This is very difficult. Thus, this data cannot be stored in a member variable of class Account. At the same time, this data should not be stored in a global variable. Then the data is liable to be changed by even non-member functions. It will also potentially lead to name conflicts. However, this means that it should be stored in a member variable of class Account!

How can this conflict be resolved? Storing the data in a static variable of the class resolves this conflict. Static data members are members of the class and not of any object of the class, that is, they are not contained inside any object.

We prefix the declaration of a variable within the class definition with the keyword static to make it static data member of the class. See Listing 2.30.

# Listing 2.30 Declaring a static data member

```
/*Beginning of Account.h*/
class Account{
    static float interest_rate; // static data member
    rest of the class Account
};
/End of Account.*/
```

A statement declaring a static data member inside a class will obviously not cause any memory to get allocated for it. Moreover, memory for a static data member will not get allocated when objects of the class are declared. This is because a static data member is not member of any object. Therefore, we must not forget to write the statement to define (allocate memory) for a static variable. Explicitly defining a static member outside the class is necessary. Otherwise, the linker produces an error. The following statement allocates memory for interest_rate member of class Account.

```
float Account::interest_rate;
```

The above statement initializes interest_rate to zero. If some other value (4.5) is desired, the statement should be rewritten as follows.

```
float Account::interest_rate=4.5;
```

Static data members should be defined in the implementation files only. The header file is included in both the implementation file and the driver program. the static data member's definition would be in two files—the library file created from the implementation file and the object file created from the driver program. But in order to get the executable, the linker will have to link these files. Upon finding two definitions of the static data member, the linker would throw an error.

Making static members private prevents any change from non-member functions as only member functions can change the values of static data members.

Introducing static data members does not increase the size of objects of the class. Static data members are not contained within objects. There is only one copy of the static data member in the memory. Let us try the following program (Listing 2.31) to find out.