# **Listing 6.16** Class Definitions in the TNode hierarchy – `ValueLeafNode`  
(in *Parser, Nodes.h*).

```
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
    TNode_UP Clone( void ) const override;
};

// A leaf with a floating-point value
using NumberLeafNode = ValueLeafNode< double >;
```
```

On lines [74–82], we see a series of definitions for the constructors and assignment operators of the `ValueLeafNode` class. Since we do not know what type will be used for V in the future, the move constructor and assignment operator are also added with the default implementation. This means the compiler will try to use move operations for the `fVal` object, if the V class has move operations and they are not throwing exceptions. For this purpose, our implementations of the move semantics are declared `noexcept`. `ValueLeafNode` is not a pure virtual class, so in the source *Visitors.cpp* file are full implementations of the `Accept` and `Clone` virtual functions declared on lines [90] and [95].

Finally, the `NumberLeafNode` alias is defined as the `ValueLeafNode` class instantiated with the double type. We can extend this idea when implementing the tree with leaves holding other types.