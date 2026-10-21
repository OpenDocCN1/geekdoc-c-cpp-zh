
- 2. A consequence of rule 1 is that there cannot be more than one constructor with different names and same arguments. If there is a need for more than one constructor, one should have a single constructor and overload it with different sets of arguments.

- 3. A constructor cannot specify a return type. Even writing void is not allowed (though a constructor always returns the object of the class it belongs to after constructing it).

> Although constructors cannot specify a return type, they always return the object of the class they belong to.

- 4. A constructor should not have a return statement in the body of the constructor.

- 5. The address of a constructor cannot be obtained. Hence, there cannot be a function pointer pointing to a constructor.

- 6. A constructor can be defined as private, but then it would not be possible to define objects using those constructors. This is because defining a constructor as private tries to execute a private function by the object at the time of definition, which is not allowed. Therefore, unless normal definition of the object is not restricted, the constructors should be defined as public.

## 5.5 DEFAULT CONSTRUCTORS

A default constructor is one with no argument or with all default arguments, that is, it is a constructor with an empty argument list or with all arguments having some default value (so that the constructor can be called without any argument). There are two different types of default constructors. When the user does not define any constructor, it is a compiler-provided default constructor, and when the user provides one, it is a user-defined one. The compiler-defined default constructor may not be synthesized by the compiler in all cases and will be synthesized only when the default constructor is necessary. The user can specify the default constructor whenever he/she wishes to do so. Usually, when a user provides a constructor, the compiler does not provide one.

### 5.5.1 Compiler-defined Default Constructor

Suppose a few objects of a class are defined but no constructors are defined for them. What will happen when that object is defined? For example, when the statement

```
student CaptainStudent;
```

is executed, what actually happens?

In such a case, memory that is sufficient for storing the complete CaptainStudent is set aside and given the name ‘CaptainStudent’. If CaptainStudent is addressed later on, the content of this address is fetched.

When the constructors are not provided by the programmers, C++ will provide the same effect by synthesizing the physical constructor code in some of the non-trivial cases. If only memory allocation for the object is to be performed, the effect is provided but the physical constructor code is not synthesized. It would be interesting to know when the physical coding of a constructor is needed, but this is beyond the scope of an introductory book. Readers are encouraged to refer to Stanly Lippman’s classic Inside the C++ Object Model for the description. For simplicity, we assume that the constructor is provided and we have the effect of construction

> When the user does not define any constructor, the compiler provides a default constructor.

of the object. This C++ constructor enables us to use the object CaptainStudent later in the program by constructing that object. Constructors of this form, which do not take any parameters, are known as default constructors.

> Note Physical constructors are not always synthesized by the compiler. However, there are a few non-trivial cases where the operation demands such synthesis.

### 5.5.2 User-defined Default Constructor

The default constructors synthesized by the compiler cannot do all the initializations that are needed for a class. The synthesized constructor only fulfils the requirements of the compiler. Even when the physical constructor is not synthesized, the compiler provides only those effects that will suit its own requirements and not that of the users. Thus, memory allocation is provided but initialization is not provided by compiler. When we define CaptainStudent, we expect a memory size good enough to hold the object and would like to use it (by storing information about the members of CaptainStudent and manipulate it). The compiler would provide that memory using this constructor. However, the compiler does not need initialization, so it is not provided by the default constructor. Initialization is the programmer’s responsibility and should be done explicitly. Consider an example of a node class for a linked list.

```
class node
{
    int Value;
    int *PtrNextValue; // Other items needed for node
}
```

In this case, suppose the node is used as follows:

```
node First;
// checking for empty list
if(First.PtrNextValue)
/* Wrong! The pointer is not initialized to null */
{
    // Necessary action
}
```

Here, consider the statement

```
node First;
```

Depending on the situation, a compiler may define a default constructor for us. However, it only provides memory allocation to store the object of type node in this case (and no physical constructor is constructed). It will certainly not initialize either Value or PtrNextValue for us. It is a programmer’s job and if they need to be initialized, the constructor must be written as follows:

> Compilers provide the additions that suit their own requirements and not that of the users.

```
class node
{
    int Value;
    int *PtrNextValue;
public:
node()
```

```
int ItemNo;
string ItemName;
public:
    Item()    // Default constructor
    {
        ItemNo = 0;
        ItemName = "";
        /* This is not required as String object is initialized already by the constructor provided in string class */
    }

    void SetDetails(int TempItemNo, string TempItemName)
    {
        ItemNo = TempItemNo;
        ItemName = TempItemName;
    }

    void ShowDetails()
    {
        cout << "\n Item number is" << ItemNo;
        cout << "\n Item name is" << ItemName;
    }
};

class ItemCollection
{
    Item ItemArray[20];
    int ItemIndex;
public:
    ItemCollection()      // Default constructor
    /* If we remove this default constructor, it will not affect the program */
    {
        for(int i=0; i<20; i++)
        ItemArray[i].SetDetails(0, "");
        ItemIndex = 0;
    }

    void SetDetails(Item TempItemArray[])
    {
        for(int i=0; i<20; i++)
        ItemArray[i] = TempItemArray[i];
    }

    void PrintDetails()
    {
        for(int i=0; i<20; i++)
        ItemArray[i].ShowDetails();
    }
};

int main()
{
    ItemCollection IC;
    Item TempItemArray[20];
    for(int i=0; i<20; i++)
    {
        TempItemArray[i].SetDetails(i, "Dummy");
    }
    IC.SetDetails(TempItemArray); IC.PrintDetails();
}
```

The readers are encouraged to try the following. Get the output of the program. Remove the default constructor of ItemCollection class and get the output again. Observe the difference.

The output does not change. This is because the default constructor is initialized to zero and " " is redundant. It is just a good programming practice to initialize, so that if one forgets to assign values to it later, one would get a value zero and " " and realize the error. When the constructor is not provided, those values are not initialized. As long as reasonable values are provided to both of them, there will not be any trouble and no significant issue is created.

The ItemCollection default constructor is anyway redundant, as Item constructor is already initializing Items.

## Cases Where a Default Constructor must be Present

Sometimes, initialization is very important and the counter begins from there. So, if a default constructor is not provided, the counter is not initialized, which will lead to an incorrect execution.

Program 5.2 is an example where the user-defined default constructor must be present.

## PROGRAM 5.2 Useful default constructor

```
//DefaultConstructor.cpp
#include <iostream>
#include <string>
using namespace std;

class Item
{
    int ItemNo;
    string ItemName;
public:
    Item()      // Default constructor
    {
        ItemNo = 0;
        ItemName = "";
        /* This is redundant as the string constructor must have done this already */
    }

    void SetDetails(int TempItemNo, string TempItemName)
    {
        ItemNo = TempItemNo;
        ItemName = TempItemName;
    }

    void ShowDetails()
    {
        cout << "\n Item number is" << ItemNo;
        cout << "\n Item name is" << ItemName;
    }
};

class ItemCollection
{
    Item ItemArray[20];
    int ItemIndex;
public:
    ItemCollection() // Default constructor
    {
