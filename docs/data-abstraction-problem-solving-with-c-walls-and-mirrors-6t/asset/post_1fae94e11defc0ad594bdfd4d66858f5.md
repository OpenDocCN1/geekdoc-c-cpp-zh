
the vector but does not give you the entry in the removed element. You must save that entry before calling pop_back. For example, the following statements determine the current size of the vector myVector, save the value in the last element, and then remove the last element from the vector:

```
int length = myVector.size(); // Find the current number of elements
string last = myVector[length - 1]; // Get the string in the last element
myVector.pop_back(); // subscripts start at 0
// Reduce the number of elements
```

A subsequent call to myVector.size() would return length - 1, since the last element was removed.

To remove all elements from a vector and leave the vector empty, you use the method clear:

```
myVector.clear(); // myVector is now an empty vector
```

clear removes all elements from a vector so it has a size of 0

After a vector has been cleared, you must use the method push_back to add new entries.
C++ Interlude 7 provides more information about vector, including these and other methods.

## A.7 Strings

Earlier, you saw that C++ provides literal character strings such as

"This is a string."

You can declare and use variables that contain such strings, and then manipulate the strings as naturally as you manipulate integers by using familiar operators. Our presentation includes only some of the possible operations on strings.

The C++ Standard Library provides the data type string. To use this library, you include the statements

```
#include <string>
using namespace std;
```

in your program.

You can declare a string variable title and initialize it to the empty string by writing

```
string title;
```

You can initialize a string variable to a string literal when you declare it by writing

```
string title = "Walls and Mirrors";
```

You can subsequently assign another string to title by using an assignment statement such as

```
title = "J Perfect's Diary";
```

In each of the previous examples, title has a length of 17. You use either of the methods length or size to determine the current length of a string. Thus, title.length() and title.size() are each 17.

You can reference the individual characters in a string by using the same index notation that you use for an array. Thus, in the previous example, title[0] contains the character J and title[16] contains the character y.

You can compare strings by using the familiar comparison operators. Not only can you see whether two strings are equal, but you can also discover which of two strings comes before the other.

- Examples of true expressions

The ordering of two strings is analogous to alphabetic ordering, but you use the ASCII table instead of the alphabet. Thus, the following relationships are all true:

```
"dig" < "dog"
"Star" < "star" (because 'S' < 's')
"start" > "star"
"d" > "abc"
```

You can concatenate two strings to form another string by using the + operator. That is, you place one string after another to form another string. For example, if

```
string str1 = "Com";
```

the statements

```
string str2 = str1 + "puter";
str1 += "puter";
```

assign the string "Computer" to each of str2 and str1. Similarly, you can append a single character to a string, as in

```
str1 += 's';
```

- Use substr to access part of a string

You can manipulate a portion of a string by using the method

```
substr(position, length)
```

The first argument specifies the position of the beginning of the substring (remember that 0 is the position of the first character in the string). The second argument is the length of the substring. For example,

```
title.substr(2, 7)
```

is the string "Perfect".

To perform input and output with C++ strings, you must include the library iostream by writing the statement

```
#include <iostream>
```

- You can use << to display a string

in your program. For example, you then can display the contents of a string variable by executing

```
title = "Walls and Mirrors";
cout << title << "\n";
```

The result is Walls and Mirrors. The operator << writes the entire string, including the blanks

- You can use >> to read a string without whitespace

You can read a string of characters into a string variable. For example, when the statement

```
cin >> title;
```

reads the data line

Jamie Perfect's Diary

it assigns the string "Jamie" to title. Whitespace in the input line terminates the read operation for a string. To read the entire line of input, including its blank characters, you write

```
getline(cin, title);
```

## A.8 Classes

Object-oriented programming, or OOP, views a program not as a sequence of actions but as a collection of components called objects that interact to produce a certain result. A group of objects of the same kind belong to a class, which is a programming construct that defines the object’s data type. Chapter 1 tells more about OOP; here we want to discuss how to write a class in C++.

An object contains data and can perform certain operations on or with that data. The class associated with a particular object describes its data and its operations. That is, a class is like a blueprint for creating certain objects. An object’s operations, or behaviors, are defined within the class by methods, which are simply functions within a class. These methods, together with the class’s data are known as the class’s members.

A C++ class defines a new data type

We could use a ball as an example of an object. Because thinking of a basketball, volleyball, tennis ball, or soccer ball probably suggests images of the game rather than the object itself, let’s abstract the notion of a ball by picturing a sphere. A sphere of a given radius has attributes such as volume and surface area. A sphere as an object should be able to report its radius, volume, surface area, and so on. That is, the sphere object has methods that return such values.

In C++, a class has the following form:

```
class Sphere
{
private:
    // Declarations of private data members and methods
    // Definitions of private methods
    ...
public:
    // Definitions of public methods
    ...
};
```

By default, all members in a class are private—they are not directly accessible by any program that uses the class—unless you designate them as public. However, explicitly indicating the private and public portions of a class is good programming practice and one that we will follow in this book. You should always declare a class’s data members as private.

Most methods are public, but private methods—which only the class can call—can be helpful, as you will see. The definition of a class’s method can call any of the class’s other methods or use any of its data members, regardless of whether they are private or public.

Classes have special methods, called constructors and destructors, for the creation and destruction of its objects. A constructor creates and initializes new objects, or instances, of a class. A destructor destroys an instance of a class, when the object’s lifetime ends. A typical class has several constructors, but only one destructor. For many classes, you can omit the destructor. In such cases, the compiler will generate a destructor for you. For now, the compiler-generated destructor is sufficient. C++ Interlude 2 discusses how and why you would write your own destructor.

An object is an instance of a class

A constructor creates and initializes an object

A destructor destroys an object

In C++, a constructor has the same name as the class. Constructors have no return type—not even void—and cannot use return to return a value. Constructors can have arguments. We discuss constructors in more detail shortly, after we look at an example of a class definition.

### A.8.1 The Header File

You should place each class definition in its own header file or specification file—whose name by convention ends in .h. The header file Sphere.h shown in Listing A-2 contains a class definition for sphere objects.

### LISTING A-2 The header file Sphere.h

```
/** @file Sphere.h */
const double PI = 3.14159;
/** Definition of a class of Spheres. */
class Sphere
{
private:
    double theRadius; // The sphere's radius
public:
    /** Default constructor: Creates a sphere and initializes
        its radius to a default value.
        Precondition: None.
        Postcondition: A sphere of radius 1 exists. */
    Sphere();
    /** Constructor: Creates a sphere and initializes
        its radius.
        Precondition: initialRadius is the desired radius.
        Postcondition: A sphere of radius initialRadius exists. */
    Sphere(double initialRadius);
    /** Sets (alters) the radius of this sphere.
        Precondition: newRadius is the desired radius.
        Postcondition: The sphere's radius is newRadius. */
    void setRadius(double newRadius);
    /** Gets this sphere's radius.
        Precondition: None.
        Postcondition: Returns the radius. */
    double getRadius() const;
    /** Gets this sphere's diameter.
        Precondition: None.
        Postcondition: Returns the diameter. */
    double getDiameter() const;
    /** Gets this sphere's circumference.
        Precondition: PI is a named constant.
        Postcondition: Returns the circumference. */
    double getCircumference() const;
    /** Gets this sphere's surface area.
        Precondition: PI is a named constant.
        Postcondition: Returns the surface area. */
    double getArea() const;
    /** Gets this sphere's volume.
        Precondition: PI is a named constant.
        Postcondition: Returns the volume. */
    double getVolume() const;
}; // end Sphere
// End of header file.
```

Comments in the header file specify the methods
