
Next, we define the `class listType` to implement a list as an ADT. Typically in a list, not only do we store the elements, but we also keep track of the number of elements in the list. Therefore, our `class listType` has two member variables: one to store the elements and another to keep track of the number of elements in the list. The following `class listType` defines the list as an ADT.

```cpp
class listType
{
public:
    bool isEmptyList() const;
    bool isFullList() const;
    int search(int searchItem) const;
    void insert(int newElement);
    void remove(int removeElement);
    void destroyList();
    void printList() const;
    listType(); //constructor

private:
    int list[1000];
    int length;
};
```

Figure 11-10 shows the UML class diagram of the class `listType`.

![](img/f97f778697507bb6fdd80c5991210cba_673_0.png)

**FIGURE 11-10** UML class diagram of the class `listType`

## A struct Versus a class

Chapter 10 defined a `struct` as a fixed collection of components, wherein the components can be of different types. This definition of components in a `struct` included only member variables. However, a C++ `struct` is very similar to a C++ `class`. As with a class, members of a `struct` can also be functions, including constructors and a destructor. The only difference between a `struct` and a `class` is that, by default, all members of a `struct` are `public`, and all members of a `class` are `private`. You can use the member access specifier `private` in a `struct` to make a member `private`.

In C, the definition of a `struct` is similar to the definition of a `struct` in C++, as given in Chapter 10. Because C++ evolved from C, the standard C-structs are perfectly acceptable in C++. However, the definition of a `struct` in C++ was expanded to include member functions and constructors and destructors. In the future, because a `class` is a syntactically separate entity, specially designed to handle an ADT, the definition of a `class` may evolve in a completely different way than the definition of a C-like `struct`.

Both C++ `classes` and `structs` have the same capabilities. However, most programmers restrict their use of structures to adhere to their C-like structure form and thus do not use them to include member functions. In other words, if all of the member variables of a `class` are `public` and the `class` has no member functions, you typically use a `struct` to group these members. This is, in fact, how it is done in this book.

## Information Hiding

The previous section defined the `class` `clockType` to implement the time in a program. We then wrote a program that used the `class` `clockType`. In fact, we combined the `class` `clockType` with the function definitions to implement the operations and the function main so as to complete the program. That is, the specification and implementation details of the `class` `clockType` were directly incorporated into the program.

Is it a good practice to include the specification and implementation details of a class in the program? Definitely not. There are several reasons for not doing so. Suppose the definition of the `class` and the definitions of the member functions are directly included in the user’s program. The user then has direct access to the definition of the class and the definitions of the member functions. Therefore, the user can modify the operations in any way the user pleases. The user can also modify the member variables of an object in any way the user pleases. Thus, in this sense, the `private` member variables of an object are no longer `private` to the object.

If several programmers use the same object in a project and if they have direct access to the internal parts of the object, there is no guarantee that every programmer will use the same object in exactly the same way. Thus, we must hide the implementation details. The user should know only what the object does, not how it does it. Hiding the implementation details frees the user from having to fit this extra piece of code in the program. Also, by hiding the details, we can ensure that an object will be used in exactly the same way throughout the project. Furthermore, once an object has been written, debugged, and tested properly, it becomes (and remains) error-free.

![](img/f97f778697507bb6fdd80c5991210cba_674_0.png)

This section discusses how to hide the implementation details of an object. For illustration purposes, we will use the class **clockType**.

To implement **clockType** in a program, the user must declare objects of type **clockType** and know which operations are allowed and what the operations do. So, the user must have access to the specification details. Because the user is not concerned with the implementation details, we must put those details in a separate file called an **implementation file**. Also, because the specification details can be too long, we must free the user from having to include them directly in the program. However, the user must be able to look at the specification details so that he or she can correctly call the functions, and so forth. We must, therefore, put the specification details in a separate file. The file that contains the specification details is called the **header file** (or **interface file**).

The implementation file contains the definitions of the functions to implement the operations of an object. This file contains, among other things (such as the preprocessor directives), the C++ statements. Because a C++ program can have only one function, main, the implementation file does not contain the function main. Only the user program contains the function main. Because the implementation file does not contain the function main, we cannot produce the executable code from this file. In fact, we produce what is called the object code from the implementation file. The user then links the object code produced by the implementation file with the object code of the program that uses the class to create the final executable code.

Finally, the header file has an extension h, whereas the implementation file has an extension cpp. Suppose the specification details of the class clockType are in a file called clockType. The complete name of this file should then be clockType.h. If the implementation details of the class clockType are in a file—say, clockTypeImp—the name of this file must be clockTypeImp.cpp.

The file clockTypeImp.cpp contains only the definitions of the functions, not the definition of the class. Thus, to resolve the problem of an undeclared identifier (such as the function names and variable names), we include the header file clockType.h in the file clockTypeImp.cpp with the help of the include statement. The following include statement is required by any program that uses the class clockType, as well as by the implementation file that defines the operations for the class clockType:

```cpp
#include "clockType.h"
```

Note that the header file clockType.h is enclosed in double quotation marks, not angular brackets. The header file clockType.h is called the user-defined header file. Typically, all user-defined header files are enclosed in double quotation marks, whereas the system-provided header files (such as iostream) are enclosed between angular brackets.

The implementation contains the definitions of the functions, and these definitions are hidden from the user because the user is typically provided *only* the object code.

However, the user of the class should be aware of what a particular function does and how to use it. Therefore, in the specification file with the function prototypes, we include comments that briefly describe the function and specify any preconditions and/or postconditions.

**Precondition:** A statement specifying the condition(s) that must be true before the function is called.

**Postcondition:** A statement specifying what is true after the function call is completed.

Following are the specification and implementation files for the class clockType:

```cpp
//clockType.h, the specification file for the class clockType

class clockType
{
public:
    void setTime(int hours, int minutes, int seconds);
        //Function to set the time.
        //The time is set according to the parameters.
        //Postcondition: hr = hours; min = minutes;
        //               sec = seconds;
        //               The function checks whether the
        //               values of hours, minutes, and seconds
        //               are valid. If a value is invalid, the
        //               default value 0 is assigned.

    void getTime(int& hours, int& minutes, int& seconds) const;
        //Function to return the time.
        //Postcondition: hours = hr; minutes = min;
        //               seconds = sec;

    void printTime() const;
        //Function to print the time.
        //Postcondition: The time is printed in the form
        //               hh:mm:ss.

    void incrementSeconds();
        //Function to increment the time by one second.
        //Postcondition: The time is incremented by one second.
        //               If the before-increment time is
        //               23:59:59, the time is reset to 00:00:00.

    void incrementMinutes();
        //Function to increment the time by one minute.
        //Postcondition: The time is incremented by one minute.
        //               If the before-increment time is
        //               23:59:53, the time is reset to 00:00:53.

    void incrementHours();
        //Function to increment the time by one hour.
        //Postcondition: The time is incremented by one hour.
        //               If the before-increment time is
        //               23:59:53, the time is reset to 00:59:53.
```
