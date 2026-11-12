
- 3. A matrix is a rectangular array of numerical values. You can add or multiply two matrices to form a third matrix. You can multiply a matrix by a scalar, and you can transpose a matrix. Design an ADT that represents a matrix that has these operations.

  Specify each ADT operation by stating its purpose, by describing its parameters, and by writing a pseudocode version of its header. Then write a C++ interface for the methods of a matrix. Include javadoc-style comments in your code.

- 4. A ring is a collection of items that has a reference to a current item. An operation—let's call it advance—moves the reference to the next item in the collection. When the reference reaches the last item, the next advance operation moves the reference back to the first item. A ring also has operations to get the current item, add an item, and remove an item. The details of where an item is added and which item is removed are up to you.

  Design an ADT to represent a ring of objects. Specify each operation by stating its purpose, by describing its parameters, and by writing a pseudocode version of its header. Then write a C++ interface for a ring's methods. Include javadoc-style comments in your code.

- 5. A set is a special bag that does not allow duplicates. Specify each operation for a set of objects by stating its purpose, by describing its parameters, and by writing preconditions, postconditions, and a pseudocode version of its header. Then write a C++ interface for the set. Include javadoc-style comments in your code.

- 6. Imagine a pile of books on your desk. Each book is so large and heavy that you can remove only the top one from the pile. You cannot remove a book from under another one. Likewise, you can add another book to the pile only by placing it on the top of the pile. You cannot add a book beneath another one.

  If you represent books by their titles alone, design a class that you can use to track the books in the pile on your desk. Specify each operation by stating its purpose, by describing its parameters, and by writing a pseudocode version of its header. Then write a C++ interface for the pile's methods. Include javadoc-style comments in your code.

This page intentionally left blank

## C++ Classes

## Contents

- C1.1 A Problem to Solve 32
- C1.1.1 Private Data Fields 33
- C1.1.2 Constructors and Destructors 33
- C1.1.3 Methods 34
- C1.1.4 Preventing Compiler Errors 35
- C1.2 Implementing a Solution 36
- C1.3 Templates 37
- C1.4 Inheritance 40
- C1.4.1 Base Classes and Derived Classes 40
- C1.4.2 Overriding Base-Class Methods 42
- C1.5 Virtual Methods and Abstract Classes 44
- C1.5.1 Virtual Methods 44
- C1.5.2 Abstract Classes 45

## Prerequisites

- Appendix A Review of C++ Fundamentals
- Chapter 1 Data Abstraction: The Walls

Throughout this book we design abstract data types and implement them as data structures using C++. This C++ Interlude provides a refresher on C++ classes and then introduces additional C++ tools we can use to define our abstract data types in a flexible manner that maintains the wall between our design and the implementation.

After reviewing classes, we will look at class templates. This C++ construct gives us the power to specify the data type of the items contained in a data structure in a very generic way. For example, if you had spent two weeks developing a great class to represent a bag of integers, wouldn't it be great if you could easily use the same code for a bag that holds strings? Class templates allow you to define classes that are independent of the type of data stored in the data structure. When a client is ready to instantiate an object of the class, the client can specify the type of data the object holds.

Header (.h), or specification, files in C++ provide a mechanism to partially separate the design of a class from the implementation in the source, or implementation (.cpp), file. The header file must also contain a description of both the data fields for the class and any private methods used by the class. A client does not need to know about the private methods or data fields to use the class in a program. To provide a public interface for an ADT, you can write an abstract base class, thereby separating design from implementation. An abstract base class allows the client to take full advantage of polymorphism when using our class.

To introduce these concepts, let's look at a simple problem that illustrates all three of the fundamental concepts of object-oriented programming: encapsulation, inheritance, and polymorphism.

## C1.1 A Problem to Solve

Suppose that a friend who is creating a video game asked you to design and develop a group of classes to represent three types of boxes carried by the characters in the game. Each type of box can only hold one item. A character can put an item in the box or look at the item in the box. The three types of boxes are:

- Plain box—a plain old box that holds only one item.
- Toy box—a box that has color and holds only one item.
- Magic box—a box that holds only one item, but magically changes it to the first item that was ever stored in the box.

Let's begin by designing an ADT plain box. It is the simplest of the three boxes, and we may be able to use aspects of its implementation for the other two boxes. Since game characters can only place items in the box or look at them, the box needs only two public methods, setItem to place an item in the box and getItem to get the stored item. Here is the UML notation for those methods:

```
+setItem(theItem: ItemType)
+getItem(): ItemType
```

We can define ItemType as the type of item stored in the box by using a typedef statement. For example, to have the box hold a double, we can write

```
typedef double ItemType;
```

To have the box hold another type of data, we need only to replace the word double with the new data type. Listing C1-1 shows the declaration of our class PlainBox that would appear in a header file. To save space here, we show only comments that describe the class element type and omit the specifications, preconditions, and postconditions. We have used the object-oriented concept of encapsulation to group together data—the item stored in the box—with the methods that operate on that data: the two constructors, a method setItem to change the item's value, and a method getItem to return the item's value.

```
LISTING C1-1 The header file for the class PlainBox
/** @file PlainBox.h */
#ifndef PLAIN_BOX
#define PLAIN_BOX
// Set the type of data stored in the box
typedef double ItemType;

// Declaration for the class PlainBox
class PlainBox
{
private:
   // Data field
   ItemType item;

public:
   // Default constructor
   PlainBox();

   // Parameterized constructor
   PlainBox(const ItemType& theItem);

   // Method to change the value of the data field
   void setItem(const ItemType& theItem);

   // Method to get the value of the data field
   ItemType getItem() const;
}; // end PlainBox

#endif
```

Let's look in detail at this C++ class declaration.

### C1.1.1 Private Data Fields

The data field `item` is declared in a private section of the class declaration. Every data field in every class presented in this textbook is in a private section. This restricts access to the data field to just the class in which it is defined. Typically, we provide methods—such as `setItem` and `getItem`—to access the data fields. In this way, the class controls how and whether other classes can access the data fields. This design principle should lead to programs that not only are easier to debug, but also have fewer logical errors from the beginning.

Clients and derived classes should not have direct access to the data fields of a class. If a class designer believes that a derived class might need to access or modify the data fields of the base class, you should still make the data fields private but provide protected methods so that any derived classes can access or modify the data. More information on access modifiers, such as private and protected, is presented in a later C++ Interlude.

As we build more complex data structures, we need to guarantee their integrity. This is simpler to do if we restrict access to the data fields to only our class. For example, suppose we have a class that stores items in an array and maintains a count of the number of items used in the array. Each time our class adds or removes an item from the array, the item count needs to be modified to reflect the change. If a client of our class had direct access to the array, the client could add and remove entries in the array and neglect to update the item counter. This counter would not accurately reflect the number of entries in the array, resulting in, for example, the loss of data or an abnormal termination of the program.

### C1.1.2 Constructors and Destructors

Classes have two types of special methods, called constructors and destructors. A **constructor** allocates memory for new instances of a class and can initialize the object's data to specified values. A **destructor** destroys an instance of a class when the object's lifetime ends. A typical class has several
