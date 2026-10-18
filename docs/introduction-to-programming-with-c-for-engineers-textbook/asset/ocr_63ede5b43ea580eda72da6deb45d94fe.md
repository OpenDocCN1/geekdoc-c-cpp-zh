The complete definition of the TNode base class starts on line [28]. This is a pure virtual class since it contains pure virtual member functions that define an abstract interface for the entire hierarchy, as shown in Figure 6.15. Hence, it is not possible to create a TNode object. This fact is reflected by the class constructor placed in the protected section of the class on line [36]. By using = default, we instruct the compiler to provide its default implementation. This makes our intentions clearer than simply providing an empty definition like {}. As we know, when designing a class hierarchy, it is important to define the base class destructor as virtual (Section 4.11). Here it is declared as pure virtual on line [44] by adding the = 0 specifier. In this case, though, it is redundant, since there are other pure virtual functions. Nevertheless, declaring a class that has no functions as pure virtual is a useful technique. Basically, for pure virtual functions, we do not even need to provide definitions (body). But some of them will be called anyway. This is the case for the base class destructor ~TNode; therefore, it needs a complete definition as well. We do not even might seem that on line [44] we could easily add the empty {} after = 0, it is forbidden by the standard (though accepted by some compilers). Therefore, this empty definition goes in the Node.cpp source file. Fortunately, the linker reports whether a pure virtual function needs a full body – i.e. if a body is required but cannot be found.

```
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
}
```