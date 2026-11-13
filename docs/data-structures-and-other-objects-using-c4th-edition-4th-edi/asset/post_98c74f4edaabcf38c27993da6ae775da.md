
## Chapter 2 Abstract Data Types and C++ Classes

> The happiest way to deal with a man is never to tell him anything he does not need to know.
> ROBERT A. HEINLEIN
> Time Enough for Love

### LEARNING OBJECTIVES

When you complete Chapter 2, you will be able to...

- specify and design new classes using a pattern of information hiding with private member variables, const member functions, and modification member functions.
- write a header file and a separate implementation file for any new class.
- create and use namespaces to organize new classes.
- use your new classes (and at least one STL class) in small test programs.
- use the automatic assignment operator and the automatic copy constructor.
- identify situations in which member functions and constructors can benefit from using default arguments.
- correctly identify and use value parameters, reference parameters, and const reference parameters.
- overload certain binary operators and input/output operators for new classes.
- identify the need for friend functions of a new class and correctly implement such nonmember functions (which are sometimes overloaded operators).
- Use STL classes, such as the pair class, in an application program.

### CHAPTER CONTENTS

- 2.1 Classes and Members
- 2.2 Constructors
- 2.3 Using a Namespace, Header File, and Implementation File
- 2.4 Classes and Parameters
- 2.5 Operator Overloading
- 2.6 The Standard Template Library and the Pair Class
- Chapter Summary
- Solutions to Self-Test Exercises
- Programming Projects

> emphasize what work is done rather than how the work is done

Object-oriented programming (OOP) is an approach to programming in which data occurs in tidy packages called objects. Manipulation of an object happens with functions called member functions, which are part and parcel of their objects.

In C++, the mechanism to create objects and member functions is called a class. Classes can support information hiding, which was presented as a cornerstone of program design in Chapter 1. Typically one programming team designs and implements a class, while other programmers use the class. The programmers that use the class have no knowledge of how the class is implemented. In fact, the implementer of a C++ class can completely hide the knowledge of how the class is implemented—resulting in ideal information hiding.

Such a strong emphasis on information hiding is motivated partly by mathematical research about how programmers can improve their reasoning about data types that are used in programs. These mathematical data types are called abstract data types, or ADTs—and therefore, programmers sometimes use the term ADT to refer to a class that is presented to other programmers with information hiding. This chapter presents two examples of such classes. The examples illustrate the features of C++ classes, with emphasis on information hiding. By the end of the chapter you will be able to implement your own classes in C++. Other programmers could use one of your classes without knowing the details of how you implemented the class.

### 2.1 CLASSES AND MEMBERS

A class is a new kind of data type. Each class that you define is a collection of data, such as integers, characters, and so on. In addition, a class has the ability to include special functions, called member functions. Member functions are incorporated into the class's definition and are designed specifically to manipulate the class. A programmer who designs a class can even mandate that the only way of manipulating the class is through its member functions. But this abstract discussion does not really tell you what a class is. We need some examples. As you read through the first example, concentrate on learning the techniques for implementing a class. Also notice features that allow you to use a class written by another programmer, without knowing the details of the class's implementation.

#### PROGRAMMING EXAMPLE: The Throttle Class

Our first example of a class is a new data type to store and manipulate the status of a simple throttle. Classes such as our throttle class appear in programs that simulate real-world objects. For instance, a flight simulator might include classes for the plane and various parts of the plane such as the engines, the rudder, the altimeter, and even the throttle.

The simple throttle that we have in mind is a lever that can be moved to control fuel flow. The throttle we have in mind has a single shutoff point (where there is no fuel flow) and a sequence of six positions where the fuel is flowing at progressively higher rates. At the topmost position, the fuel flow is fully on. At the intermediate positions, the fuel flow is proportional to the location of the lever. For example, with six possible positions, and the lever in the fourth position, the fuel flows at 3/6 of its maximum rate.

One function provided with the class permits a program to initialize a throttle to its shutoff position. Once the throttle has been initialized, there is another function to shift the throttle lever by a given amount.

We also have two functions to examine the status of a throttle. The first of these functions returns the amount of fuel currently flowing, expressed as a proportion of the maximum flow. For example, this function will return approximately 0.667 when the six-position throttle is in its fourth position. The other function returns a true-or-false value, telling whether the throttle is currently on (that is, whether the lever is above the zero position). Thus, the throttle has a total of four functions:

- 1. A function to set a throttle to its shutoff position
- 2. A function to shift a throttle's position by a given amount
- 3. A function that returns the fuel flow, expressed as a proportion of the maximum flow
- 4. A function to tell us whether the throttle is currently on

We can define this new data type as a “class” called throttle that includes data (to store the throttle’s current position) and the four functions to modify and examine the throttle. Once the new class is defined, a programmer can declare objects of type throttle and manipulate those objects with the functions. Here is the class definition:

```cpp
class throttle
{
public:
    // MODIFICATION MEMBER FUNCTIONS
    void shut_off();
    void shift(int amount);
    // CONSTANT MEMBER FUNCTIONS
    double flow() const;
    bool is_on() const;
private:
    int position;
};
```

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_62_0.png)

four throttle functions

declaring the throttle class

This class definition defines a new data type called throttle. The new data type is a class, meaning that it may have some components that are data and other components that are functions. Let's examine the definition piece by piece.

**The class head.** The head of the definition consists of the C++ keyword class, followed by the name of the new class. You may use any legal identifier for the class name. We chose the name throttle. We use nouns for the names of new classes—this isn't required by C++, but it's a part of our documentation standard (Appendix J).

**The member list.** The rest of the definition, from the opening bracket to the closing semicolon, is the member list of the definition.

**The public section.** The first part of the member list is called the public section. It begins with the C++ keyword public followed by a colon and a list of items. These items are available to anyone who uses the new data type. For the throttle, the list contains the four functions. Such functions are called member functions to distinguish them from ordinary functions. Another term is method, which means the same as "member function." When a member function is listed in a class body, we list only the function's prototype (that is, the head followed by a semicolon). For example, one of the throttle function prototypes is:

```cpp
void shift(int amount);
```

The prototype indicates that the function has one parameter (an integer called amount). We will use this function to shift a throttle's lever up or down by a given amount. The implementation of the shift function does not appear in the class definition; it will appear elsewhere with other function implementations. One of the other throttle functions has the following prototype:

```cpp
bool is_on();
```

the bool type

This function can be used to determine whether a throttle is currently on. The return value of the function has the data type bool, which is a built-in data type provided in the ANSI/ISO C++ Standard. The bool data type is intended solely for true-or-false values (also called boolean values or logical values). The important properties of the bool type are shown in Figure 2.1. If your compiler does not support the bool type, then see Appendix E, "Dealing with Older Compilers," for alternatives.

public member functions

Anyone who declares a variable of type throttle can manipulate that throttle with the four public member functions. In fact, these four functions are the only way that a throttle may be manipulated, since there is nothing else available in the public section of the definition.

modification member functions

You should notice that we have classified the public member functions into two groups. The first two functions, shut_off and shift, are modification member functions. A modification member function can change the value of an object. For the throttle, the modification functions can change the position of the throttle's lever.
