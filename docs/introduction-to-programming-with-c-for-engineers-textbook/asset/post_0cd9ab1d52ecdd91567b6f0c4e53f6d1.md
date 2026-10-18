
## 6.6.4.2 Implementation of the `TNode` Hierarchy and Cooperation with Visitors

Before we dive into the code, we will explain a special relation between all the nodes and the visitor design pattern that will be used to traverse the tree. The two are interrelated: nodes call visitors, and visitors call functions from the nodes. Thus the two groups know about each other. But we cannot simply add their header files to each other - one has to be first. To overcome this problem, something needs to be defined first. In C++, this can be solved by properly arranging the header files and by using only prior declarations of the interrelated classes, with their full definitions provided elsewhere. In the `Nodes.h` header shown in Listing 6.15, we see such declarations at the beginning on lines [9, 13]. These are the declarations of `TVisitor` and `TNode`. The first will be used later. But why do we need a declaration of `TNode` if the definition follows in a few lines? This is necessary to define two important and different pointer types. The first, defined on line [17], is `Node_UP`, which is an alias to the smart pointer `std::unique_ptr` that defines the _owning_ relation. That is, the `Node_UP` type will be used to hold pointers to `TNode`-like objects, which they are responsible for deleting at the proper time, as discussed in Section 5.3. On the other hand, on line [20], a simple `NodePtr` non-owning pointer to `TNode` is defined. This type is used whenever access to a `TNode` object is required to perform an action, access its data, and so on, but not to delete it.

![](img/31dee73f41f3d43a1f2e2b4eaffa2afd_464_0.png)

The complete definition of the `TNode` base class starts on line [28]. This is a pure virtual class since it contains pure virtual member functions that define an abstract interface for the entire hierarchy, as shown in Figure 6.15. Hence, it is not possible to create a `TNode` object. This fact is reflected by the class constructor placed in the protected section of the class on line [36]. By using `= default`, we instruct the compiler to provide its default implementation. This makes our intentions clearer than simply providing an empty definition like `{}`. As we know, when designing a class hierarchy, it is important to define the base class destructor as virtual (Section 4.11). Here it is declared as pure virtual on line [44] by adding the `= 0` specifier. In this case, though, it is redundant, since there are other pure virtual functions. Nevertheless, declaring a class that has no functions as pure virtual is a useful technique. Basically, for pure virtual functions, we do not even need to provide definitions (body). But some of them will be called anyway. This is the case for the base class destructor `~TNode`; therefore, it needs a complete definition as well. It might even seem that on line [44] we could easily add the empty `{}` after `= 0`; it is forbidden by the standard (though accepted by some compilers). Therefore, this empty definition goes in the `Node.cpp` source file. Fortunately, the linker reports whether a pure virtual function needs a full body – i.e. if a body is required but cannot be found.

```cpp
#pragma once
#include <memory>
#include <cassert>

// Forward class declarations
class TVisitor;

// A forward declaration of the base class for the node hierarchy.
class TNode;

// Owning relation - we can declare the std::unique_ptr
// with only declared class TNode. Its definition follows.
using Node_UP = std::unique_ptr< TNode >;

// Non-owning relation
using NodePtr = TNode *;

// This is an interface class representing a node
// in the tree - it serves only
// to be derived from, its objects cannot be created.
class TNode
{
protected:
    // Making the constructor protected is also
    // a way to indicate a class as a base since
    // only derived classes can be instantiated.
    TNode( void ) = default;

public:

    // To indicate the class is an abstract interface
    // its destructor is a pure virtual function
    // what is indicated by adding = 0 to the declaration.
    virtual ~TNode() = 0;

public:

    // Pure virtual functions can have implementation
    // but it is not absolutely required.
    // Derived types must provide their own implementation if they
    // are instantiated.
    // Accept allows operation of a visitor.
    virtual void Accept( TVisitor & v ) const = 0;

public:

    // Re-create yourself - No implementation
    // for Clone in the base class.
    virtual Node_UP Clone( void ) const = 0;
};
```

In the `TNode` class and its hierarchy are two distinctive pure virtual functions whose roles we need to explain, as follows:

- **Accept** pure virtual function, declared on line [53], provides *a common interface* for the broad group of *visitors*. These are objects that will let us traverse a tree by visiting each of its nodes in a certain order. Accept is called, providing one of the visitor objects as its parameter. This, in turn, is passed alongside the tree to perform its job, whatever it is. The good news is that due to dynamic polymorphism, one Accept per `TNode` class is enough to accept the entire hierarchy of various visitors, even those that will be devised in the future. We will return to this issue when discussing the visitor hierarchy.
- The purpose of the second pure virtual function **Clone**, declared on line [59], is to define a mechanism for creating a *complete duplicate* of any object from the `TNode` hierarchy based on a simple pointer to its *prototype*. Such behavior can be achieved by providing Clone in each class derived from the `TNode`. Due to its behavior, this mechanism is called a *prototype design pattern* (Gamma et al. 1994).

We will see these two in all classes derived from `TNode`.

## 6.6.4.3 Implementation of the `ValueLeafNode` Class

Now let’s visit another member of the `TNode` hierarchy. This is the template `ValueLeafNode` class, whose definition starts in Listing 6.16, lines [64, 65]. It is responsible for storing the value `fVal` of type V, as shown on line [70]. Objects of this class represent leaves, such as those shown in Figure 6.14. Being a template class makes it easy to define leaves that store non-numeric values. This can be an abstract name of a variable whose value is stored in a look-up table, for instance.

**Listing 6.16** — Class Definitions in the `TNode` hierarchy – `ValueLeafNode` (in *Parser, Nodes.h*).

```cpp
// A leaf (an object) with a value such as
// a number, a string, etc.
template < typename V >
class ValueLeafNode : public TNode
{

private:

    V       fVal {};    // a held value

public:

    ValueLeafNode( void ) : fVal( ) {}
    explicit ValueLeafNode( const V & val ) : fVal( val ) {}

    virtual ~ValueLeafNode() = default;

    ValueLeafNode( const ValueLeafNode & ) = default;
    ValueLeafNode( ValueLeafNode && ) noexcept = default;
    ValueLeafNode & operator = ( const ValueLeafNode & ) = default;
    ValueLeafNode & operator = ( ValueLeafNode && ) noexcept = default;

public:

    V GetValue( void ) const { return fVal; }

    // Accept a visitor
    void Accept( TVisitor & v ) const override;

public:

    // Re-create yourself
    Node_UP Clone( void ) const override;
};

// A leaf with a floating-point value
using NumberLeafNode = ValueLeafNode< double >;
```

On lines [74–82], we see a series of definitions for the constructors and assignment operators of the `ValueLeafNode` class. Since we do not know what type will be used for V in the future, the move constructor and assignment operator are also added with the default implementation. This means the compiler will try to use move operations for the `fVal` object, if the V class has move operations and they are not throwing exceptions. For this purpose, our implementations of the move semantics are declared `noexcept`. `ValueLeafNode` is not a pure virtual class, so in the source *Visitors.cpp* file are full implementations of the `Accept` and `Clone` virtual functions declared on lines [90] and [95].

Finally, the `NumberLeafNode` alias is defined as the `ValueLeafNode` class instantiated with the double type. We can extend this idea when implementing the tree with leaves holding other types.
