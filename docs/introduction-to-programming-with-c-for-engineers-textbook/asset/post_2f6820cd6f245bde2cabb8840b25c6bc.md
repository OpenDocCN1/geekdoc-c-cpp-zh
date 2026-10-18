
## 5.3.1.4 Constructions to Avoid When Using `unique_ptr`

Finally, let’s discuss a few things to be aware of when using `unique_ptr`. When defining `unique_ptr`, we can use `auto` to automatically infer types and to avoid typing. But this is possible only when using `make_unique`, as shown here:

```cpp
// AClass object on the heap, p_d takes care
auto p_d_0( new AClass( "No" ) );    // oops, an ordinary pointer

delete p_d_0;                         // get rid of it
```

If we forget about `make_unique` and leave only `auto`, then an ordinary pointer is generated, as on line [2]. It will not be guarded by a `unique_ptr`, so it must be explicitly destroyed, as on line [4]. On the other hand, a `unique_ptr` can be created directly by a return of the new operator or as mentioned with `make_unique`:

```cpp
// AClass object on the heap, p_d takes care
auto p_d_0( make_unique< AClass >( "Yes" ) );
```

We should also be very careful not to create a `unique_ptr` from an ordinary pointer since it is possible to create more than one `unique_ptr` holding a link to a single object. Inevitably this will cause a program error when we try to call `delete` more than once on the same memory location.

```cpp
AClass * p_d_5 = new AClass;

unique_ptr< AClass > p_d_6( p_d_5 );       // do not initialize via ord pointer

// ...
// somewhere else ...
unique_ptr< AClass > p_d_7( p_d_5 );       // wrong, two unique_ptr to one object
```

Finally, we must avoid creating a `unique_ptr` on the heap with the new operator. For some reason, in the SL, the new operator was not forbidden for `unique_ptr`.

## 5.3.2 (⚔) More on `shared_ptr` and `weak_ptr`

In this section, we show how to use the `shared_ptr` and `weak_ptr` smart pointers when creating a doubly connected list, as shown in Figure 5.1. `shared_ptr` cannot be used in two directions because such a construction would make the two objects dependent on each other. In effect, both objects cannot be deleted, which will result in a memory leak despite using smart pointers. To overcome such mutual dependencies, the `weak_ptr` comes to play. In our example in Listing 5.4, a backward connection is created by using `weak_ptr`. Let’s analyze the code: it consists mainly of the N class, which defines a single node, and a function showing the process of creating and using a list.

```cpp
void double_linked_list_test( void )
{
    using SP_N = shared_ptr< N >;    // a useful type alias
    SP_N root, pr;    // two empty shared ptrs
    // --------------------
    // Create the list
    for( const auto & s : { "A", "B", "C", "D", "E", "F" } )
    {
    if( pr == false )
    {
    root = pr = make_shared< N >( s );    // the first node
    }
    else
    {
    // Make a new node, and connect to the previous node in the list
    pr->SetNext( make_shared< N >( s, pr );
    pr = pr->GetNext();    // advance pr on to the end of the list
    }
    }
    // --------------------
    // Ok, the list is ready, so traverse the list and call operator()
    // To check if pointing at a valid object, implicitly use operator bool ()
    for( SP_N p = root; p; p = p->GetNext() )
    cout << ( * p )() << endl;
}
```

The list is created based on an initializer list provided in the `for` loop on line [45]. Then we have two possibilities: either we are adding the very first node, in which case line [49] is executed; or we are adding new nodes to an existing list, on lines [54-55]. Going into detail, first a new node is created, which is identified by a shared pointer. This is used to initialize the `fNext` pointer of the current object at the end of the list. Then, we move the end of the list to the just-created object. After the list is ready, the string-composing function is called from each node in the list, as on lines [63-64]. The whole list is traversed, and at each node, the previous, current, and next nodes are accessed to concatenate their strings. A node may be at one end of the list, so each time we access a node, we need to check whether the pointers are pointing at valid objects. The output of our function looks as follows:

> AB
> ABC
> BCD
> CDE
> DEF
> EF
> Killing node A
> Killing node B
> Killing node C
> Killing node D
> Killing node E
> Killing node F
> Killing node F

Notice that the borderline nodes produce shortened output. After the list is processed, the objects are automatically deleted thanks to the shared pointers, in the order in which were created, from A to F.

Finally, note that the SL offers the `std::list` class, which implements the list data structure. Therefore, if we need the standard list functionality, we can use a ready and verified solution instead of writing our own code. The `std::list` class will be used and presented in Section 6.1.

## 5.4 Summary

## Things to Remember

+   - In general, do not use low-level memory management with `new` and `delete`. Instead, use the SL containers (e.g. `vector`, `array`) and/or smart pointers
+   - If you are not sure which smart pointer to use, think first of using the `unique_ptr`
+   - Use `make_unique` functions to create `unique_ptr`s
+   - When changing old code, try to refactor all calls to `new` into smart pointers. In addition, try to refactor all calls to `auto_ptr` into calls to modern smart pointers (`unique_ptr` should be the first candidate)
+   - Do not make things more complicated than they should be – if all you need is a general-purpose buffer on the heap, then use a vector instead of a smart pointer

## Questions and Exercises

+   1. Explain the main idea behind using smart pointers.

+   2. Explain the main differences between `unique_ptr` and `smart_ptr`.

+   3. A *ternary tree* is a data structure in which each node can have up to three children (https://en.wikipedia.org/wiki/Ternary_tree). Such structures are used, for example, for spell-checking. In such a case, the node also contains a one-letter data member. Implement a ternary tree composed of objects like the N class in Listing 5.4. Each node should have `unique_ptr` members to link to its three children.

+   4. In the following code snippet, identify the object dependency arising on line [25]:

```
#include <iostream>
#include <memory>

// Cyclic dependence problem

struct Bar;

struct Foo
{
    std::shared_ptr<Bar> bar;
    ~Foo() { std::cout << "~Foo()\n"; }
};

struct Bar
{
    std::shared_ptr<Foo> foo;
};

void CyclicPointersProblem_Test( void )
{
    auto foo = make_shared< Foo >();
    foo->bar = make_shared< Bar >();

    foo->bar->foo = foo;        // oops, a circle ...
}
```

Remove the circular dependency between the objects. Hint: change the type of the smart pointer on line [16].

+   5. Design and implement a simple memory-allocation method for an embedded system. For safety reasons, a single statically allocated memory block can be used from which all partitions resulting from memory requests are created. Hint: read about and then implement the buddy algorithm (https://en.wikipedia.org/wiki/Buddy_memory_allocation).

+   6. Design and implement a class to represent a submatrix (https://en.wikipedia.org/wiki/Matrix_(mathematics)) in a matrix object using the proxy pattern, presented in Section 4.15.5. The proxy has no data of its own but operates on the data of its associated matrix. But it defines its own local coordinate system and behaves like any other matrix. Hint: after making some modifications to the EMatrix class in Listing 4.7, derive a proxy class to represent submatrices. Such a proxy should not allocate its own data but should be constructed with a reference to its associated matrix. Accessing an element in the submatrix should result in the data coordinates being transformed to the coordinate system of the associated matrix.

[PAGE 394]

You are ready to learn about more methods and techniques of object-oriented programming in C++. Congratulations! In this chapter, we will present programming topics such as processing regular expressions, implementing state machines, building our own libraries, the filesystem, system clock and time measurement, ranges and functional programming, expression parsing, syntax trees, and the composite and interpreter design patterns, all complete with code examples.

We have already implemented many classes and created many objects. Usually, these have been related to real objects expressed with nouns, such as TQuadEq or TLongNumber. However, objects can also represent actions expressed with verbs, such as do_this or compare_that. In such cases, the central part of the object is a function: do_this or compare_that. Sometimes these are accompanied by data. Although not obligatory, if the main goal of a class is to represent a particular action or a function, this is usually implemented using the overloaded functional operator (). Objects of such classes are called functional objects or functors. A call to such an overloaded operator () resembles a call to a simple function, as mentioned in Section 3.14.9. In this section, we will investigate an interrupt-like component to handle various actions that are invoked in response to different external events. Such a component may be a part of an embedded system or, with minor modifications, can serve as a menu-handling module, for instance.

Figure 6.1 shows an event array with attached lists of handlers, performing various actions on an event. The actions are in the form of user-derived classes from the THandler base class with the overloaded virtual operator (). Actions for each event, such as a system interrupt, are arranged as dynamic lists. That is, actions can be added to and also removed from the lists.

Listing 6.1 presents code implementing the event system shown in Figure 6.1. All the definitions are enclosed inside the EventSystem namespace. The THandler class, whose the definition starts on line [6], constitutes the base class for all actions in the system. Not surprisingly, actions are implemented by overloading functional operators in the classes derived from THandler. For this purpose, on line [16], THandler defines the overloaded operator () as a pure virtual function, which is indicated with the = 0 suffix (Section 5.3.1.2). This also means THandler is intended only to be a base class that defines an abstraction for the entire hierarchy (here, this is an abstraction of calls). As we already know, the base class’s destructors should also be defined virtual. In THandler, this is achieved on line [11]. But interestingly enough, ~THandler is
