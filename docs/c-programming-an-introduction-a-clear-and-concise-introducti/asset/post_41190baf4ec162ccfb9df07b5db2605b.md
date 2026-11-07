
methods can have the same name as long as there are specific differences in the parameter lists of the two methods. This is called *method overloading*. This difference has to be in the number and types of parameters in the parameter list. For example, we can have two constructor methods called Name in the Name class because one constructor has an empty parameter list (the default constructor) and the other constructor has 3 string parameters.

Using the rules of overloading, we can have the following constructor methods for the Name class (only the headings are supplied here):

```cpp
Name();

Name(string firstName, string middleName, string lastName);

Name(string firstName, string lastName);

Name(string lastName);
```

Each of these methods has a different number of parameters in the parameter list, so when the compiler sees a call to one of them, it can differentiate it from the other method definitions.

Now let's look at a complete definition for all of these constructors:

```cpp
Name()
{
    first = "";
    middle = "";
    last = "";
}

Name(string firstName, string middleName,
     string lastName)
{
    first = firstName;
    middle = middleName;
    last = lastName;
}

Name(string firstName, string lastName)
{
    first = firstName;
    middle = "";
    last = lastName;
}

Name(string lastName)
{
    first = "";
    middle = "";
    last = lastName;
}
```

The Name constructor with two parameters will create an object with a first and last name and just the empty string for the middle name, while the last constructor will create an object with empty string for the first and middle names and the passed-in value for the last name. Of course, the last constructor was just picked because it is just assumed that a Name object would not be created with just a first or a middle name and not a last name.

## Class Get and Set Methods

Once an object has been created, and data stored in the members, you need ways to get data into and out of the object. A well-designed class provides a group of methods that return member values from the object and assign values to the members. These are called get and set methods.

Let’s start with set methods. We looked at one example of a set method earlier, the setName() method. This method sets the values of all the members in one method call. We also need set methods for each individual member. Here are the set methods we need for the Name class:

```cpp
void setFirst(string firstName)
{
    first = firstName;
}

void setMiddle(string middleName)
{
    middle = middleName;
}

void setLast(string lastName)
{
    last = lastName;
}
```

Now, if a Name object has a name change that doesn't involve the whole name, we can call whichever of the set methods we need. For example:

```cpp
Name myName("Mary", "Alice", "Smith");
cout << myName.displayName() << endl;
// Mary gets married to Joe Brown
myName.setLast("Brown");
cout << myName.displayName() << endl;
```

The output is:

```
Mary Alice Smith
Mary Alice Brown
```

We also need methods that return the information individually, and not just as a group, as getName() does. Get methods provide this capability. Here are the get methods for the Name class:

```cpp
string getFirst()
{
    return first;
}

string getMiddle()
{
    return middle;
}

string getLast()
{
    return last;
}
```

This little program fragment shows how to use the get methods:

```cpp
cout << "The first name in myName is: " <<
     myName.getFirst() << endl;
cout << "The middle name in myName is: " <<
     myName.getMiddle() << endl;
cout << "The last name in myName is: " << myName.getLast()
     << endl;
```

The output from this code fragment is:

```
The first name in myName is: Mary
The middle name in myName is: Alice
The last name in myName is: Brown
```

## Other Class Methods

Besides the standard class methods that all classes need (constructor methods, get methods, and set methods), a class may also need other methods in order to define the complete behavior of the class.

An example of a method we might need in the Name class is a method that returns a Name object's initials. We don't need to create a member for this piece of data because we can get it from the members we already have. We just need to pull the first character from the first name, middle name, and last name. Here is the definition for the getInitials() method:

```cpp
string getInitials()
{
    return first.substr(0,1) + middle.substr(0,1)
        + last.substr(0,1);
}
```

A call to the method:

```cpp
cout << myName.getInitials() << endl;
```

will return:

```
MAB
```

You can place this definition anywhere in the public area of the class definition, but these types of methods are usually placed after the get and set methods.

```cpp
}
Name(string lastName)
{
    first = "";
    middle = "";
    last = lastName;
}

void setFirst(string firstName)
{
    first = firstName;
}

void setMiddle(string middleName)
{
    middle = middleName;
}

void setLast(string lastName)
{
    last = lastName;
}

void setName(string firstName, string middleName,
             string lastName)
{
    first = firstName;
    middle = middleName;
    last = lastName;
}

string getFirst()
{
    return first;
}

string getMiddle()
{
    return middle;
}

string getLast()
{
    return last;
}

string getName()
{
    return first + " " + middle + " " + last;
}

string getInitials()
{
    return first.substr(0,1) +
           middle.substr(0,1) +
           last.substr(0,1);
}
};

int main(array<System::String ^> ^args)
{
    Name myName("Mary", "Alice", "Smith");
    cout << myName.getName() << endl;
    // Mary gets married to Joe Brown
    myName.setLast("Brown");
    cout << myName.getName() << endl;
    cout << "The first name in myName is: "
         << myName.getFirst()
         << endl;
    cout << "The middle name in myName is: "
         << myName.getMiddle() << endl;
    cout << "The last name in myName is: "
         << myName.getLast() << endl;
    cout << "myName's initials are: "
         << myName.getInitials() << endl;
    Console::ReadKey();
    return 0;
}
```

```cpp
void setName(string, string, string);
```

When the class is compiled, the definition of the method in the source file has to match the prototype in the header file exactly or the compiler will issue an error.

To create a header file for the Name class using Visual C++ Express, right-click on Header Files in the Solution Explorer window, select Add, and then select New Item. Choose Header File for the item type and name it “Name.h”. An empty code editor window will appear and you can put the header file code there.

Here is the header file for the Name class:

```cpp
#include <string>
using namespace std;

class Name
{
private:
    string first, last, middle;

public:
    Name();
    Name(string, string, string);
    Name(string, string);
    Name(string);
    void setFirst(string);
    void setMiddle(string);
    void setLast(string);
    void setName(string, string, string);
    string getFirst();
    string getMiddle();
    string getLast();
    string getName();
    string getInitials();
};
```

Even though there is no executable code in the header file, we still need to include the string library since the string data type is mentioned in several places.

It is important that every member and method used in the source file must be defined in the header file or the compiler will issue an error when compiling the class.

## Creating the Source File for the Name Class

After you've built the header file, the next step is to build a source file that contains the executable code definitions for the class methods. To create a source file in Visual C++ Express, right-click on Source Files in the Solution Explorer, select Add, then select New Item and choose C++ File as the item type. Name the file "Name.cpp". In fact, the name of the source file has to match the name of the header file exactly.

The source file for the Name class looks almost exactly like what we built for the class definition above. The source file for the Name class is listed below, followed by an explanation of what is different about the code here versus what we used for the Name class above:

```cpp
#include "stdafx.h"
using namespace System;

#include "Name.h"

Name::Name()
{
    first = "";
    middle = "";
    last = "";
}

Name::Name(string firstName, string middleName,
            string lastName)
{
    first = firstName;
    middle = middleName;
```
