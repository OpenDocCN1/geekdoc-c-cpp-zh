# 13. Interfaces

An interface defines a contract. A class or struct that implements an interface must adhere to its contract. An interface may inherit from multiple base interfaces, and a class or struct may implement multiple interfaces.

> **BILL WAGNER** Interfaces work best when they are small in scope and few in number. Larger interfaces create more work for implementers. Larger numbers of interfaces provide more opportunities for ambiguity and collisions.

> **ERIC LIPPERT** The trope that interfaces are contracts is undoubtedly both useful and frequently stated. It’s worth pointing out an interface is actually a pretty weak way to represent a contract. All an interface tells you is which methods are available, what their names are, which types they take, and which types they return. Nothing whatsoever about the semantics of the operation is represented in the contract: that an object complying with this contract must be disposed aggressively, that Drive() throws an exception if not called after StartEngine(), that the first parameter must be null and the second parameter must be non-zero, and so on. All that stuff goes in the documentation, not somewhere that an analysis tool can dig into. The new code contract system that ships with version 4.0 of the CLR enables you both to specify contracts in more detail than interfaces do alone and to do interesting analysis on these contracts at compile time.

Interfaces can contain methods, properties, events, and indexers. The interface itself does not provide implementations for the members that it defines. The interface merely specifies the members that must be supplied by classes or structs that implement the interface.

# 13.1 Interface Declarations

An interface-declaration is a type-declaration (§9.6) that declares a new interface type.