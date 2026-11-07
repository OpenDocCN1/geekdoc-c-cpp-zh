
data is always added to or deleted from the top of the stack. For example, C++ programs use a stack to manage automatic variables. As new automatic variables are generated, they are added to the top of the stack. When they expire, they are removed from the stack.

Let’s look at the properties of a stack in a general, abstract way. First, a stack holds several items. (That property makes it a *container*, an even more general abstraction.) Next, a stack is characterized by the operations you can perform on it:

- You can create an empty stack.
- You can add an item to the top of a stack (that is, you can *push* an item).
- You can remove an item from the top (that is, you can *pop* an item).
- You can check whether the stack is full.
- You can check whether the stack is empty.

You can match this description with a class declaration in which the public member functions provide an interface that represents the stack operations. The private data members take care of storing the stack data. The class concept is a nice match to the ADT approach.

The private section has to commit itself to how to hold the data. For example, you can use an ordinary array, a dynamically allocated array, or some more advanced data structure, such as a linked list. However, the public interface should hide the exact representation. Instead, it should be expressed in general terms, such as creating a stack, pushing an item, and so on. Listing 10.10 shows one approach. It assumes that the `bool` type has been implemented. If it hasn’t been implemented on your system, you can use `int`, `0`, and `1` rather than `bool`, `false`, and `true`.

Listing 10.10  **stack.h**

```cpp
// stack.h -- class definition for the stack ADT
#ifndef STACK_H_
#define STACK_H_

typedef unsigned long Item;

class Stack
{
private:
    enum {MAX = 10};    // constant specific to class
    Item items[MAX];    // holds stack items
    int top;            // index for top stack item
public:
    Stack();
    bool isempty() const;
    bool isfull() const;
    // push() returns false if stack already is full, true otherwise
    bool push(const Item & item);    // add item to stack
```

```cpp
while (cin.get() != '\n')
    continue;
if (!isalpha(ch))
{
    cout << '\a';
    continue;
}
switch(ch)
{
    case 'A':
    case 'a': cout << "Enter a PO number to add: ";
              cin >> po;
              if (st.isfull())
                  cout << "stack already full\n";
              else
                  st.push(po);
              break;
    case 'P':
    case 'p': if (st.isempty())
                  cout << "stack already empty\n";
              else {
                  st.pop(po);
                  cout << "PO #" << po << " popped\n";
              }
              break;
}
cout << "Please enter A to add a purchase order,\n"
     << "P to process a PO, or Q to quit.\n";
}
cout << "Bye\n";
return 0;
}
```

The little while loop in Listing 10.12 that gets rid of the rest of the line isn’t absolutely necessary at this point, but it will come in handy in a modification of this program in Chapter 14. Here’s a sample run:

```text
Please enter A to add a purchase order,
P to process a PO, or Q to quit.
A
Enter a PO number to add: 17885
Please enter A to add a purchase order,
P to process a PO, or Q to quit.
P
PO #17885 popped
Please enter A to add a purchase order,
P to process a PO, or Q to quit.
A
Enter a PO number to add: 17965
Please enter A to add a purchase order,
P to process a PO, or Q to quit.
A
Enter a PO number to add: 18002
Please enter A to add a purchase order,
P to process a PO, or Q to quit.
P
PO #18002 popped
Please enter A to add a purchase order,
P to process a PO, or Q to quit.
P
PO #17965 popped
Please enter A to add a purchase order,
P to process a PO, or Q to quit.
P
stack already empty
Please enter A to add a purchase order,
P to process a PO, or Q to quit.
Q
Bye
```

## Summary

OOP emphasizes how a program represents data. The first step toward solving a programming problem by using the OOP approach is to describe the data in terms of its interface with the program, specifying how the data is used. Next, you need to design a class that implements the interface. Typically, private data members store the information, whereas public member functions, also called methods, provide the only access to the data. The class combines data and methods into one unit, and the private aspect accomplishes data hiding.

Usually, you separate a class declaration into two parts, typically kept in separate files. The class declaration proper goes into a header file, with the methods represented by function prototypes. The source code that defines the member functions goes into a methods file. This approach separates the description of the interface from the details of the implementation. In principle, you need to know only the public class interface to use the class. Of course, you can look at the implementation (unless it's been supplied to you in compiled form only), but your program shouldn’t rely on details of the implementation, such as knowing that a particular value is stored as an int. As long as a program and a class communicate only through methods defining the interface, you are free to improve either part separately without worrying about unforeseen interactions.

A class is a user-defined type, and an object is an instance of a class. This means an object is a variable of the type or the equivalent of a variable, such as memory allocated by new according to the class specification. C++ tries to make user-defined types as similar as possible to standard types, so you can declare objects, pointers to objects, and arrays of objects. You can pass objects as arguments, return them as function return values, and assign one object to another of the same type. If you provide a constructor method, you can initialize objects when they are created. If you provide a destructor method, the program executes that method when the object expires.

Each object holds its own copies of the data portion of a class declaration, but they share the class methods. If mr_object is the name of a particular object and try_me() is a member function, you invoke the member function by using the dot member operator: mr_object.try_me(). OOP terminology describes this function call as sending a try_me message to the mr_object object. Any reference to class data members in the try_me() method then applies to the data members of the mr_object object. Similarly, the function call i_object.try_me() accesses the data members of the i_object object.

If you want a member function to act on more than one object, you can pass additional objects to the method as arguments. If a method needs to refer explicitly to the object that evoked it, it can use the this pointer. The this pointer is set to the address of the evoking object, so *this is an alias for the object itself.

Classes are well matched to describing ADTs. The public member function interface provides the services described by an ADT, and the class’s private section and the code for the class methods provide an implementation that is hidden from clients of the class.

## Chapter Review

1. What is a class?
2. How does a class accomplish abstraction, encapsulation, and data hiding?
3. What is the relationship between an object and a class?
4. In what way, aside from being functions, are class function members different from class data members?
5. Define a class to represent a bank account. Data members should include the depositor’s name, the account number (use a string), and the balance. Member functions should allow the following:
   - Creating an object and initializing it.
   - Displaying the depositor’s name, account number, and balance
   - Depositing an amount of money given by an argument
   - Withdrawing an amount of money given by an argument

Just show the class declaration, not the method implementations. (Programming Exercise 1 provides you with an opportunity to write the implementation.)
