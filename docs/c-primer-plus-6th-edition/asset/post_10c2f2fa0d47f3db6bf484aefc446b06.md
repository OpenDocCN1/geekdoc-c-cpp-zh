
14. What's wrong, if anything, with the following code?

```cpp
class Kitchen
{
  private:
    double kit_sq_ft;
  public:
    Kitchen(){kit_sq_ft = 0.0; }
    virtual double area() const { return kit_sq_ft * kit_sq_ft; }
};
class House : public Kitchen
{
  private:
    double all_sq_ft;
  public:
    House(){all_sq_ft += kit_sq_ft;}
    double area(const char *s) const { cout << s; return all_sq_ft; }
}
```

# Programming Exercises

- 1. Start with the following class declaration:
```cpp
// base class
class CD { // represents a CD disk
private:
  char performers[50];
  char label[20];
  int selections; // number of selections
  double playtime; // playing time in minutes
public:
  CD(char *si, char *s2, int n, double x);
  CD(const CD & d);
  CD();
  CD(const CD & d);
  void Report() const; // reports all CD data
  CD & operator=(const CD & d);
};
```
Derive a Class that adds an array of char members that will hold a string identifying the primary work on the CD. If the base class requires that any functions be virtual, modify the base-class declaration to make it so. If a declared method is not needed, remove it from the definition. Test your product with the following program:

```cpp
#include <iostream>
using namespace std;
#include "classic.h" // which will contain #include cd.h

void Bravo(const Cd & disk);
int main()
{
    Cd cd1("Beatles"
```

- 2. Do Programming Exercise 1 use dynamic memory allocation instead of fixed-size arrays for the various strings tracked by the two classes.

- 3. Revise the baseDMA-lacksDMA-hasDMA hierarchy so that all three classes are derived from an ABC. Test the result with a program similar to the one in Listing 13.10. That is, it should feature an array of pointers to the ABC and allow the user to make runtime decisions as to what type of objects are created. Virtual View() methods to the class definitions to handle displaying the data.

- 4. The Benevolent Order of Programmers maintains a collection of bottled port. To describe it, the BOP Portmaster has devised a Port class, as declared here:

```cpp
#include <iostream>
using namespace std;
class Port {
private:
    char * brand;
    char style[20]; // i.e. tawny, ruby, vintage
    int bottles;
public:
    Port(const char * br = "none", const char * st = "none", int b = 0);
    Port(const Port &p); // copy constructor
    ~Port() { delete [] brand; };
    Port &operator=(const Port & p);
    Port &operator+=(int b); // adds b to bottles
    Port &operator-=(int b); // subtracts b from bottles
    int bottleCount() const { return bottles; }
    virtual void Show();
    friend ostream &operator<<(ostream & os, const Port & p);
};
```
The Show() method presents information in the following format:
Brand: tawny
Kind: Noble
Bottles: 20

The operator<<() function presents information in the following format (with no newline at the end):
tawny,20

The Portmaster completed the method definitions for the Port class and then derived the VirtualPort class as follows:

```cpp
class VirtualPort : public Port // style = "vintage"
private:
    char * nickname; // i.e., "The Noble" or "Old Velvet"
    int year;
public:
    VirtualPort();
    VirtualPort(const char * br, int b, const char * nn, int y);
    VirtualPort(const VirtualPort & vp);
    ~VirtualPort() { delete [] nickname; }
    VirtualPort &operator=(const VirtualPort & vp);
    void Show() const;
    friend ostream &operator<<(ostream & os, const VirtualPort & vp);
};
```
You get the job of completing VirtualPort work. Your first task is to recreate the Port method definitions. Your second task is to explain why certain methods are redefined and others are not. Your third task is to explain why operator() and operator<<() are not virtual. Your fourth task is to provide definitions for VirtualPort methods.

# Reusing Code in C++

In this chapter you'll learn about the:
- Has-a relationships
- Classes with member objects (containment)
- The vararray class
- Private and protected inheritance
- Multiple inheritance
- Virtual base classes
- Creating class templates
- Using class templates
- Template specializations

One of the main goals of C++ is to facilitate the reuse of code. Public inheritance is one mechanism for achieving this, but it's not the only one. This chapter investigates other choices. One technique is to use class members that are objects of another class. This is referred to as containment or composition. Another option is to use private or protected inheritance. Private and protected inheritance are typically used to implement has-a relationships—for example, a class might have an object of another class. Multiple inheritance lets you create classes that inherit from two or more base classes, combining their functionality. Chapter 10, "Objects and Classes," introduces function templates. In this chapter we will look at class templates, which provide another way of reusing code. A class template defines a class in generic terms. Then you can use the template to create specific classes for specific types. For example, you could define a general stack template and then use the template to create one class that represents a stack of int values and another class that represents a stack of double values. You could even generate a class that represents a stack of stacks.

# Classes with Object Members

Let’s begin with classes that include class objects as members. Some classes, such as the string class or the standard C++ class templates discussed in Chapter 16, "The string Class and the Standard Template Library," offer convenient ways of representing components of a more extensive class. Let’s look at a particular example now.

What is a student? Someone enrolled in a school? Someone engaged in thoughtful investigation? A refugee from exigencies of the real world? Someone with an identifying name and a set of quiz scores? Clearly, the last definition is totally inadequate characterization of a person, but it is well suited for a simple computer representation. So develop a student class based on that definition.

Simplifying a student to a name and a set of quiz scores using a class with two members: one to represent the name and one to represent the scores. For the name, you could use a char pointer and dynamic memory allocation. However, as Chapter 12, "Classes and Dynamic Memory Allocation," illustrates, that requires a lot of supporting code. Better, you could use an object of a class for someone who has already done the work. For example, you could use an object of the string class (see Chapter 12) or of the standard C++ class. The simpler is the string class because the C++ library already provides all the implementation code as well as a proper implementation. To use the string class, you’d have to make the string.cpp file part of your project.

Representing the quiz scores presents similar choices. You could use a fixed-size array, which places a size limitation on your code. You could use your own design of a class, using dynamic memory allocation to represent an array. You could look for a standard C++ class library that is capable of representing the data.

Developing your own class is not out of the question. A simple version wouldn’t be difficult because using an array of double shares many similarities with an array of char, so you could base the design of an array-of-double class on the string class. And in fact, that is what earlier editions of this book did.

But, of course, it is even easier if the library already provides a suitable class, and it does: the vararray class.

# The vararray Class: A Quick Look

The vararray class is supported by the vararray header file. As its name suggests, the class is targeted to deal with numeric values (or classes with similar properties), it supports operations such as summing the contents and finding the largest and smallest values in an array. So that it can handle different data types, vararray is defined as a template class. Later, this chapter goes into how to define template classes, but all you need to know now is how to use one.
