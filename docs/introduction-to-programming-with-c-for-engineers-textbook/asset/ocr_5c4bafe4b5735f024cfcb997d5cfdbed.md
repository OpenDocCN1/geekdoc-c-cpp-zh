```
```cpp
// Object copying disallowed by the base class

public:

    void Accept( TVisitor & v ) const override;

public:

    // Re-create yourself
    Node_UP Clone( void ) const override;
};
```
```

The implementation of the Accept member is very simple and the same for all objects of the TNode hierarchy. It is shown in Listing 6.19 for PlusOperator.

# **Listing 6.19** Implementation of the Accept member function for PlusOperator (in *Parser, Nodes.cpp*). The implementation is identical for all other nodes in the TNode hierarchy.

```
```cpp
void PlusOperator::Accept( TVisitor & v ) const
{
    v.Visit( * this );
}
```
```

Accept reverts the call to a given visitor object, providing a pointer this to this node object as its parameter. Such call reverting is enough for visitor v since, based on the type of this, an appropriate overloaded Visit function will be invoked due to polymorphism. This is the double-dispatching mechanism; we will return to it when describing visitor objects in Section 6.6.7. See also the class diagram from Figure 6.17.

On the other hand, the role and implementation of the Clone member function are covered in the next section.

# 6.6.4.6  Deep Copying Node Objects – The Prototyping Mechanism

Whereas copying objects containing data – such as NumberLeafNode – is not a problem, and we can even leave code generation for this action to the compiler by specifying = default, there is an inherent problem with copying objects containing pointers to other objects, such as PlusOperator. Simply copying pointers is usually undesirable since we end up with two different objects with references to the same data (Section 4.6.3). Therefore, all binary operations implemented with classes derived from BinOperator are disallowed any copying and moving operations by defining their copy and move members as = delete. So, in the following code snippet, only the first line compiles:

```
```cpp
PlusOperator    p1, p2;        // ok
PlusOperator    p3( p2 );      // Compiling error - no copy constructible
p1 = p2;                       // Compiling err - no copy by assignment
```
```

Imagine that we need to duplicate a tree, composed of a number of nodes of different types, having only a pointer to that tree’s root node. Such a task might be needed to launch two independent tree annotators, for instance. How do we traverse such a tree, and create a copy of each node and