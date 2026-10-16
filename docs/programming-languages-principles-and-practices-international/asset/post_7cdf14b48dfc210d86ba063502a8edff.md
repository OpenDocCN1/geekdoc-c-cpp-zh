
```cpp
class A{

// A C++ class

public:

// all public members here

protected:

// all protected members here

private:

// all private members here

};
```

(Note the final semicolon after the closing bracket, which is a vestige of C syntax; a list of variable names could appear before this semicolon, with the preceding class definition as their data type.)

In C++, initialization of objects is given as in Java by constructors that have the same name as that of the class. Constructors are automatically called when an object is allocated space in memory, and actual parameters to the constructor are evaluated at that time. Thus, constructors are similar to Java, except that in C++ objects need not be references, and so a constructor can be automatically called as part of a declaration, as well as in a new expression. Unlike Java, C++ does not have required built-in garbage collection, and so C++ also includes destructors, which like constructors have the same name as the class, but which are preceded by the tilde symbol "~" (sometimes used in logic to mean "not"). Destructors are automatically called when an object is deallocated (either by going out of scope or through the use of the delete operator), but they must be provided by the programmer and so represent a manual approach to memory deallocation.

A class declaration in C++ does not always contain the implementation code for all member functions. Member functions can be implemented outside the declaration by using the scope resolution operator indicated by a double colon "::" after the class name. It gets its name from the fact that it causes the scope of the class declaration to be reentered. Member functions that are given implementations in a class declaration are automatically assumed to be inline (that is, a compiler may replace the function call by the actual code for the function).

As a first example in C++, we offer a partial definition of a complex number class:

```cpp
class Complex{

public:

// Constructor
Complex(double r = 0, double i = 0)
: re(r), im(i) { }
```

means that **re** is initialized to the value of **r** and **im** is initialized to the value of **i**. In other words, the above code has essentially the same meaning as:

```cpp
Complex(double r = 0, double i = 0){
    re = r; im = i;
}
```

The constructor is also defined with default values given for its parameters:

```cpp
Complex(double r = 0, double i = 0)
```

This allows Complex objects to be created with 0, 1, or 2 parameters, and avoids the need to create different overloaded constructors:

```cpp
Complex i(0,1);  // i constructed as (0,1)
Complex y;       // y constructed as default (0,0)
Complex x(1);    // x constructed as (1,0)
```

### 5.4.2 Using a Template Class to Implement a Generic Collection

You saw how a generic collection class is defined in Java in Section 5.3.2. A similar feature, called **template classes**, is used to define generic collections in C++. Although the standard template library (STL) of C++ includes several built-in collection classes, let’s develop a LinkedStack class to see how a C++ template class works.

Our C++ LinkedStack class has the same basic interface as the Java version discussed in Section 5.3.2. Here is a short C++ program that exercises some of its capabilities:

```cpp
#include <iostream>
using std::cout;
using std::endl;
#include "LinkedStack.c"

int main(){
    int number;
    LinkedStack<int> stack;
    for (number = 1; number <= 5; number++)
        stack.push(number);
    cout << "The size is " << stack.size() << endl;
    while (stack.size() != 0)
        cout << stack.pop() << " ";
    cout << endl;
}
```

As you can see, this code declares a stack type in a similar manner to the Java version, although in this case the **int** type can be specified directly as the stack’s element type. However, unlike in Java, a new **LinkedStack** object is automatically created and assigned to the **stack** variable upon the mere mention of that variable in the declaration. Otherwise, the usage of **LinkedStack** is exactly the same as in the Java example.

Our Java version of LinkedStack exploited inheritance and polymorphism by extending an AbstractCollection class, which provided higher-level functionality and an interface to other collection classes. Lacking this class in C++, we define LinkedStack as a top-level class. Our C++ version includes a constructor, a destructor (more on this in a moment), the public stack instance methods, a nested node type, and a helper method to allocate and initialize a new node. Here is the code for the class:

```cpp
template <class E> class LinkedStack{

    public:

    // Constructor
    LinkedStack()
    : top(0), mySize(0) {}

    // Destructor
    ~LinkedStack(){
        while (size() > 0)
            pop();
    }

    E peek(){
        return top->data;
    }

    E pop(){
        E element = top->data;
        node * garbage = top;
        top = top->next;
        mySize -= 1;
        delete garbage;    // Must return node storage to the heap
        return element;
    }

    void push(E element){
        top = getNode(element, top);
        mySize += 1;
    }

    int size(){
        return mySize;
    }

    private:

    // The node type for LinkedStack
    struct node{
        E data;
        node* next;
    };

    // Data members for LinkedStack
    node* top;
    int mySize;

    // Helper method to initialize a new node
    node* getNode(E data, node * next){
        node * newNode = new node;
        newNode->data = data;
        newNode->next = next;
        return newNode;
    }

};
```

The notation `template <class E>` in the class header introduces the type parameter E for the stack’s element type. This parameter will be filled in with an actual C++ type in the client program’s code at compile time. The constructor and public instance methods are similar to those of the Complex class discussed earlier.

However, because the LinkedStack class utilizes dynamic storage for its nodes, it should also include a destructor. The job of this method is to return each node to the system heap when the LinkedStack object is no longer accessible from the client program (for example, when a function that creates a temporary stack returns from its call). The destructor accomplishes this by popping the stack until it is empty. The pop method, in turn, manually returns the node just removed from the linked structure to the system heap, by using the delete operator. Because C++ has no automatic garbage collection, failure to recycle storage in this manner constitutes a memory leak, which can lead to memory problems in production situations.

Note also that the node type is a C-style struct, but could have been defined as a C++ class instead. Because a node is just a private container for a datum and a link, the use of a struct and a private method getNode that builds and returns a pointer to the initialized node works just as well.

Finally, the use of explicit C-style pointers rather than references illustrates another difference between Java and C++. Even if we had defined a Node class in C++, we would still have had to use the * operator to indicate a link to the next node and a pointer variable to the node itself.

### 5.4.3 Static Binding, Dynamic Binding, and Virtual Functions

Dynamic binding of member functions is provided as an option in C++, but it is not the default. All member functions are statically bound, at compile time. Only functions defined using the keyword `virtual` are candidates for dynamic binding. For example, if we want to redefine an area function for a square derived from a rectangle, we would do so as follows in C++:

```cpp
class Rectangle{
    public:
        virtual double area(){
            return length * width;
        }
        ...
    private:
        double length,width;
};

class Square : public Rectangle{
    public:
        double area(){            // redefines rectangle::area dynamically
            return width * width;
        }
        ...
};
```

Of course, what we really want in this example is an abstract area function in an abstract class ClosedFigure. This can be achieved in C++ by the use of a so-called pure virtual declaration:

```cpp
class ClosedFigure{            // an abstract class
    public:
        virtual double area() = 0; // pure virtual
        ...
};

class Rectangle : public ClosedFigure{
    public:
        double area(){
            return length * width; }
```
