
```
/*
Generated output:

5
11
hello hello
*/
```

A completely different way to read and write streams may be implemented using `streambuf` members. All considerations mentioned so far remain valid (e.g., before a read operation following a write operation `seekg` must be used). When `streambuf` objects are used, either an `istream` is associated with the `streambuf` object of another `ostream` object, or an `ostream` object is associated with the `streambuf` object of another `istream` object. Here is the previous program again, now using *associated streams*:

```cpp
#include <iostream>
#include <fstream>
#include <string>
using namespace std;

void err(char const *msg);       // see earlier example
void err(char const *msg, long value);

void read(istream &index, istream &strings)
{
    index.clear();
    strings.clear();

    // insert the body of the read() function of the earlier example
}

void write(ostream &index, ostream &strings)
{
    index.clear();
    strings.clear();

    // insert the body of the write() function of the earlier example
}

int main()
{
    ifstream index_in("index", ios::trunc | ios::in | ios::out);
    ifstream strings_in("strings", ios::trunc | ios::in | ios::out);
    ostream index_out(index_in.rdbuf());
    ostream strings_out(strings_in.rdbuf());

    cout << "enter ‘r <number>’ to read line <number> or "
            "‘w <line>’ to write a line\n"
            "or enter ‘q’ to quit.\n";

    while (true)
    {
        cout << "r <nr>, w <line>, q ? ";       // show prompt

        string cmd;

        cin >> cmd;                             // read cmd

        if (cmd == "q")                        // process the cmd.
            return 0;

        if (cmd == "r")
            read(index_in, strings_in);
        else if (cmd == "w")
            write(index_out, strings_out);
        else
            cout << "Unknown Command: " << cmd << '\n';
    }
}
```

In this example

- the streams associated with the `streambuf` objects of existing streams are not `ifstream` or `ofstream` objects but basic `istream` and `ostream` objects.

- The `streambuf` object is not defined by an `ifstream` or `ofstream` object. Instead it is defined outside of the streams, using a `filebuf` (cf. section [14.8](#)) and constructions like:

    ```cpp
    filebuf fb("index", ios::in | ios::out | ios::trunc);
    istream index_in(&fb);
    ostream index_out(&fb);
    ```

- An `ifstream` object can be constructed using stream modes normally used with `ofstream` objects. Conversely, an `ofstream` object can be constructed using stream modes normally used with `ifstream` objects.

- If `istream` and `ostream` share a `streambuf`, then their read and write pointers (should) point to the shared buffer; they are tightly coupled.

- The advantage of using an external (separate) `streambuf` over a predefined `fstream` object is (of course) that it opens the possibility of using stream objects with specialized `streambuf` objects. These `streambuf` objects may specifically be constructed to control and interface particular devices. Elaborating this (see also section [14.8](#)) is left as an exercise to the reader.

## Chapter 7

## Classes

The C programming language offers two methods for structuring data of different types. The C struct holds data members of various types, and the C union also defines data members of various types. However, a union’s data members all occupy the same location in memory and the programmer may decide on which one to use.

In this chapter classes are introduced. A class is a kind of struct, but its contents are by default inaccessible to the outside world, whereas the contents of a C++ struct are by default accessible to the outside world. In C++ structs find little use: they are mainly used to aggregate data within the context of classes or to define elaborate return values. Often a C++ struct merely contains plain old data (POD, cf. section 9.9). In C++ the class is the main data structuring device, by default enforcing two core concepts of current-day software engineering: data hiding and encapsulation (cf. sections 3.2.1 and 7.1.1).

The union is another data structuring device the language offers. The traditional C union is still available in C++, but the C++11 standard adds unrestricted unions to the language. Unrestricted unions are unions whose data fields may be of class types. The C++ Annotations covers these unrestricted unions in section 12.5, after having introduced several other new concepts of C++.

C++ extends the C struct and union concepts by allowing the definition of member functions (introduced in this chapter) within these data types. Member functions are functions that can only be used with objects of these data types or within the scope of these data types. Some of these member functions are special in that they are always, usually automatically, called when an object starts its life (the so-called constructor) or ends its life (the so-called destructor). These and other types of member functions, as well as the design and construction of, and philosophy behind, classes are introduced in this chapter.

We step-by-step construct a class Person, which could be used in a database application to store a person’s name, address and phone number.

Let’s start by creating a class Person right away. From the onset, it is important to make the distinction between the class interface and its implementation. A class may loosely be defined as ‘a set of data and all the functions operating on those data’. This definition is later refined but for now it is sufficient to get us started.

A class interface is a definition, defining the organization of objects of that class. Normally a definition results in memory reservation. E.g., when defining an `int` variable the compiler ensures that some memory is reserved in the final program storing variable’s values. Although it is a definition, no memory is set aside by the compiler once it has processed the class definition. But a class definition follows the one definition rule: in C++ entities may be defined only once. As a class definition does not imply that memory is being reserved, the term class interface is preferred instead.

Class interfaces are normally contained in a class header file, e.g., `person.h`. We’ll start our class Person interface here (cf. section 7.6 for an explanation of the `const` keywords behind some of the class’s member functions):

```cpp
#include <string>

class Person
{
    std::string d_name;        // name of person
    std::string d_address;     // address field
    std::string d_phone;       // telephone number
    size_t      d_mass;        // the mass in kg.

public:                       // member functions
    void setName(std::string const &name);
    void setAddress(std::string const &address);
    void setPhone(std::string const &phone);
    void setMass(size_t mass);

    std::string const &name()    const;
    std::string const &address() const;
    std::string const &phone()   const;
    size_t mass()                const;
};
```

The member functions that are *declared* in the interface must still be implemented. The implementation of these members is properly called their definition.

In addition to the member function a class defines the data manipulated by the member functions. These data are called the *data members*. In Person they are `d_name`, `d_address`, `d_phone` and `d_mass`. Data members should be given private access rights. Since the class uses private access rights by default they may simply be listed at the top of the interface.

All communication between the outer world and the class data is routed through the class’s member functions. Data members may receive new values (e.g., using `setName`) or they may be retrieved for inspection (e.g., using `name`). Functions merely returning values stored inside the object, not allowing the caller to modify these internally stored values, are called *accessors*.

Syntactically there is only a marginal difference between a class and a struct. Classes by default define *private* members, structs define *public* members. Conceptually, though, there are differences. In C++ structs are used in the way they are used in C: to aggregate data, which are all freely accessible. Classes, on the other hand, hide their data from access by the outside world (which is aptly called *data hiding*) and offer member functions to define the communication between the outer world and the class’s data members.

Following Lakos (Lakos, J., 2001) **Large-Scale C++ Software Design** (Addison-Wesley), I suggest the following setup of class interfaces:

- All data members have *private access rights*, and are placed at the top of the interface.

- All data members start with `d_`, followed by a name suggesting their meaning (in chapter 8 we’ll also encounter data members starting with `s_`).

- Non-private data members *do exist*, but one should be hesitant to define non-private access rights for data members (see also chapter 13).

- Two broad categories of member functions are *manipulators* and *accessors*. *Manipulators* allow the users of objects to modify the internal data of the objects. By convention, manipulators start with `set`. E.g., `setName`.

- With *accessors*, a get-prefix is still frequently encountered, e.g., `getName`. However, following the conventions promoted by the **Qt** (see http://www.trolltech.com) *Graphical User Interface Toolkit*, the get-prefix is now deprecated. So, rather than defining the member `getAddress`, it should simply be named `address`.
