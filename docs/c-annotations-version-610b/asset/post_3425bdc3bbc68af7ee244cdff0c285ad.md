
Of the using directive, this latter person is now by implication also using namespace special, which could produce unwanted or unexpected effects:

```cpp
#include <flaw.h>
#include <iostream>

using std::cout;

int main()
{
    cout << "starting\n";      // won’t compile
}
```

The compiler is confronted with two interpretations for cout: first, because of the using directive in the flaw.h header file, it considers cout a std::cout; second, because of the using directive in the user program, it considers cout a std::ostream. Consequently, the compiler reports an error.

As a rule of thumb, header files intended for general use should not contain using declarations. This rule does not hold true for header files which are only included by the sources of a class: here the programmer is free to apply as many using declarations as desired, as these directives never reach other sources.

### 7.11 sizeof applied to class data members (C++11)

In the C++11 standard the sizeof operator can be applied to data members of classes without the need to specify an object as well. Consider:

```cpp
class Data
{
    std::string d_name;
    ...
};
```

To obtain the size of Data’s d_name member C++11 allows the following expression:

```cpp
sizeof(Data::d_name);
```

However, note that the compiler observes data protection here as well. sizeof(Data::d_name) can only be used where d_name may be visible as well, i.e., by Data’s member functions and friends.

## Chapter 8: Static Data And Functions

In the previous chapters we provided examples of classes where each object had its own set of data members. Each of the class’s member functions could access any member of any object of its class.

In some situations it may be desirable to define *common data fields*, that may be accessed by all objects of the class. For example, the name of the startup directory, used by a program that recursively scans the directory tree of a disk. A second example is a variable that indicates whether some specific initialization has occurred. In that case the object that was constructed first would perform the initialization and would set the flag to ‘done’.

Such situations are also encountered in C, where several functions need to access the same variable. A common solution in C is to define all these functions in one source file and to define the variable `static`: the variable name is invisible outside the scope of the source file. This approach is quite valid, but violates our philosophy of using only one function per source file. Another C-solution is to give the variable in question an unusual name, e.g., `_6ulav8`, hoping that other program parts won’t use this name by accident. Neither the first, nor the second legacy C solution is elegant.

**C++** solves the problem by defining `static` members: data and functions, common to all objects of a class and (when defined in the private section) inaccessible outside of the class. These static members are this chapter’s topic.

Static members cannot be defined as virtual functions. A virtual member function is an ordinary member in that it has a `this` pointer. As static member functions have no `this` pointer, they cannot be declared virtual.

### 8.1  Static data

Any data member of a class can be declared `static`; be it in the public or private section of the class interface. Such a data member is created and initialized only once, in contrast to non-static data members which are created again and again for each object of the class.

Static data members are created as soon as the program starts. Even though they’re created at the very beginning of a program’s execution cycle they are nevertheless true members of their classes.

It is suggested to prefix the names of *static* member with `s_` so they may easily be distinguished (in class member functions) from the class’s data members (which should preferably start with `d_`).

Public static data members are global variables. They may be accessed by *all* of the program’s code, simply by using their class names, the scope resolution operator and their member names. Example:

```cpp
class Test
{
        static int s_private_int;
public:
        static int s_public_int;
};

int main()
{
        Test::s_public_int = 145;   // OK
        Test::s_private_int = 12;   // wrong, don't touch
                                      // the private parts
}
```

The example does not present an executable program. It merely illustrates the *interface*, and not the *implementation* of static data members, which is discussed next.

#### 8.1.1  Private static data

To illustrate the use of a static data member which is a private variable in a class, consider the following:

```cpp
class Directory
{
        static char s_path[];

public:
        // constructors, destructors, etc.
};
```

The data member `s_path[]` is a private static data member. During the program’s execution only one `Directory::s_path[]` exists, even though multiple objects of the class Directory may exist. This data member could be inspected or altered by the constructor, destructor or by any other member function of the class Directory.

Since constructors are called for each new object of a class, static data members are not *initialized* by constructors. At most they are *modified*. The reason for this is that static data members *exist before* any constructor of the class has been called. Static data members are initialized when they are defined, outside of any member function, exactly like the initialization of ordinary (non-class) global variables.

The definition and initialization of a static data member usually occurs in one of the source files of the class functions, preferably in a source file dedicated to the definition of static data members, called `data.cc`.

The data member `s_path[]`, used above, could thus be defined and initialized as follows in a file `data.cc`:

```cpp
#include "directory.ih"

char Directory::s_path[200] = "/usr/local";
```

In the class interface the static member is actually only *declared*. In its implementation (definition) its type and class name are explicitly mentioned. Note also that the size specification can be left out of the interface, as shown above. However, its size is (either explicitly or implicitly) required when it is defined.

Note that *any* source file could contain the definition of the static data members of a class. A separate `data.cc` source file is advised, but the source file containing, e.g., `main()` could be used as well. Of course, any source file defining static data of a class must also include the header file of that class, in order for the static data member to be known to the compiler.

A second example of a useful private static data member is given below. Assume that a class `Graphics` defines the communication of a program with a graphics-capable device (e.g., a VGA screen). The initialization of the device, which in this case would be to switch from text mode to graphics mode, is an action of the constructor and depends on a static flag variable `s_nobjects`. The variable `s_nobjects` simply counts the number of `Graphics` objects which are present at one time. Similarly, the destructor of the class may switch back from graphics mode to text mode when the last `Graphics` object ceases to exist. The class interface for this `Graphics` class might be:

```cpp
class Graphics
{
    static int s_nobjects;              // counts # of objects

public:
    Graphics();
    ~Graphics();                        // other members not shown.
private:
    void setgraphicsmode();             // switch to graphics mode
    void settextmode();                 // switch to text-mode
};
```

The purpose of the variable `s_nobjects` is to count the number of objects existing at a particular moment in time. When the first object is created, the graphics device is initialized. At the destruction of the last `Graphics` object, the switch from graphics mode to text mode is made:

```cpp
int Graphics::s_nobjects = 0;          // the static data member

Graphics::Graphics()
{
    if (!s_nobjects++)
        setgraphicsmode();
}

Graphics::~Graphics()
{
    if (!--s_nobjects)
        settextmode();
}
```

Obviously, when the class `Graphics` would define more than one constructor, each constructor would need to increase the variable `s_nobjects` and would possibly have to initialize the graphics mode.

#### 8.1.2  Public static data

Data members could also be declared in the public section of a class. This, however, is deprecated (as it violates the principle of data hiding). The static data member `s_path[]` (cf. section 8.1) could be declared in the public section of the class definition. This would allow all the program’s code to access this variable directly:

```cpp
int main()
{
    getcwd(Directory::s_path, 199);
}
```

A declaration is not a definition. Consequently the variable `s_path` still has to be defined. This implies that some source file still needs to contain `s_path[]` array’s definition.
