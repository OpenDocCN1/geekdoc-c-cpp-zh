
```cpp
};
class Analyzer
{
    friend void sync(Analyzer & a, const Probe & p);  // sync a to p
    friend void sync(Probe & p, const Analyzer & a);  // sync p to a
    ...
};

// define the friend functions
inline void sync(Analyzer & a, const Probe & p)
{
    ...
}
inline void sync(Probe & p, const Analyzer & a)
{
    ...
}
```

The forward declaration enables the compiler to know that `Analyzer` is a type when it reaches the friend declarations in the `Probe` class declaration.

## Nested Classes

In C++, you can place a class declaration inside another class. The class declared within another is called a *nested class*, and it helps avoid name clutter by giving the new type class scope. Member functions of the class containing the declaration can create and use objects of the nested class. The outside world can use the nested class only if the declaration is in the public section and if you use the scope-resolution operator. (Older versions of C++ either don’t allow nested classes or implement the concept incompletely.)

Nesting classes is not the same as containment. Recall that containment means having a class object as a member of another class. Nesting a class, on the other hand, does not create a class member. Instead, it defines a type that is known just locally to the class that contains the nested class declaration.

The usual reasons for nesting a class are to assist in the implementation of another class and to avoid name conflicts. The Queue class example in Listing 12.10 in Chapter 12, “Classes and Dynamic Memory Allocation,” provides a disguised case of nested classes by nesting a structure definition:

```cpp
class Queue
{
private:
// class scope definitions
    // Node is a nested structure definition local to this class
    struct Node {Item item; struct Node * next;};
    ...
};
```

Because a structure is a class whose members are public by default, Node really is a nested class. However, this definition doesn’t take advantage of class abilities. In particular, it lacks an explicit constructor. Let’s remedy that now.

First, you need to find where Node objects are created in the Queue example. Examining the class declaration (see Listing 12.10) and the method definitions (see Listing 12.11) reveals that the only place in which Node objects are created is in the enqueue() method:

```cpp
bool Queue::enqueue(const Item & item)
{
    if (isfull())
        return false;
    Node * add = new Node;  // create node
    // on failure, new throws std::bad_alloc exception
    add->item = item;       // set node pointers
    add->next = NULL;
    ...
}
```

This code explicitly assigns values to the Node members after creating a Node. This is the sort of work that is more properly done by a constructor.

Knowing now where and how a constructor should be used, you can provide an appropriate constructor definition:

```cpp
class Queue
{
    // class scope definitions
        // Node is a nested class definition local to this class
        class Node
        {
        public:
            Item item;
            Node * next;
            Node(const Item & i) : item(i), next(0) { }
        };
        ...
};
```

This constructor initializes the node’s item member to i and sets the next pointer to 0, which is one way of writing the null pointer in C++. (Using NULL would require including a header file that defines NULL. Users of a C++11-compliant compiler can use nullptr.) Because all nodes created by the Queue class have next initially set to the null pointer, this is the only constructor the class needs.

Next, you need to rewrite enqueue() by using the constructor

```cpp
bool Queue::enqueue(const Item & item)
{
    if (isfull())
        return false;
    Node * add = new Node(item);  // create, initialize node
    // on failure, new throws std::bad_alloc exception
    ...
}
```

This makes the code for enqueue() a bit shorter and a bit safer because it automates initialization rather than requiring the programmer to correctly remember what should be done.

This example defines the constructor in the class declaration. Suppose you wanted to define it in a methods file, instead. In that case, the definition must reflect that the Node class is defined within the Queue class. This is accomplished by using the scope-resolution operator twice:

```cpp
Queue::Node::Node(const Item & i) : item(i), next(0) { }
```

## Nested Classes and Access

Two kinds of access pertain to nested classes. First, where a nested class is declared controls the scope of the nested class; that is, it establishes which parts of a program can create objects of that class. Second, as with any class, the public, protected, and private sections of a nested class provide access control to class members. Where and how a nested class can be used depends on both scope and access control. Let’s examine these points further.

### Scope

If a nested class is declared in a private section of a second class, it is known only to that second class. This applies, for example, to the Node class nested in the Queue declaration in the preceding example. Hence, Queue member functions can use Node objects and pointers to Node objects, but other parts of a program don’t even know that the Node class exists. If you were to derive a class from Queue, Node would be invisible to that class, too, because a derived class can’t directly access the private parts of a base class.

If the nested class is declared in a protected section of a second class, it is visible to that class but invisible to the outside world. However, in this case, a derived class would know about the nested class and could directly create objects of that type.

If a nested class is declared in a public section of a second class, it is available to the second class, to classes derived from the second class, and, because it’s public, to the outside world. However, because the nested class has class scope, it has to be used with a class qualifier in the outside world. For example, suppose you have this declaration:

```cpp
class Team
{
public:
    class Coach { ... };
    ...
};
```

Now suppose you have an unemployed coach, one who belongs to no team. To create a Coach object outside the Team class, you can use this:

```cpp
Team::Coach forhire;  // create a Coach object outside the Team class
```

These same scope considerations apply to nested structures and enumerations, too. Indeed, many programmers use public enumerations to provide class constants that can be used by client programmers. For example, the many implementations of classes defined to support the iostream facility use this technique to provide various formatting options, as you’ve already seen (and will explore more fully in Chapter 17, “Input, Output, and Files”). Table 15.1 summarizes scope properties for nested classes, structures, and enumerations.

Table 15.1 **Scope Properties for Nested Classes, Structures, and Enumerations**

| Where Declared in Nesting Class | Available to Nesting Class | Available to Classes Derived from the Nesting Class | Available to the Outside World |
|---|---|---|---|
| Private section | Yes | No | No |
| Protected section | Yes | Yes | No |
| Public section | Yes | Yes | Yes, with class qualifier |

### Access Control

After a class is in scope, access control comes into play. The same rules govern access to a nested class that govern access to a regular class. Declaring the Node class in the Queue class declaration does not grant the Queue class any special access privileges to the Node class, nor does it grant the Node class any special access privileges to the Queue class. Thus, a Queue class object can access only the public members of a Node object explicitly. For that reason, the Queue example makes all the members of the Node class public. This violates the usual practice of making data members private, but the Node class is an internal implementation feature of the Queue class and is not visible to the outside world. That’s because the Node class is declared in the private section of the Queue class. Thus, although Queue methods can access Node members directly, a client using the Queue class cannot do so.

In short, the location of a class declaration determines the scope or visibility of a class. Given that a particular class is in scope, the usual access control rules (public, protected, private, friend) determine the access a program has to members of the nested class.

## Nesting in a Template

You’ve seen that templates are a good choice for implementing container classes such as the Queue class. You may be wondering whether having a nested class poses any problems to converting the Queue class definition to a template. The answer is no. Listing 15.5
