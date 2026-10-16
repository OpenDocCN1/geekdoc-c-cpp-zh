Q: Why not make all class members public?

A: Because it goes against the idea of encapsulation.

Q: What is encapsulation?

A: The quality of being self-contained. In the world of OOP, encapsulation prevents client code from directly accessing the internals of an object. Instead, it encourages client code to use a defined interface to the object.

Q: What are the benefits of encapsulation?

A: In the world of OOP, encapsulation protects the integrity of an object. For example, you might have a spaceship object with a fuel data member. By preventing direct access to this data member, you can guarantee that it never becomes an illegal value (such as a negative number).

Q: Should I provide access to data members through accessor member functions?

A: Some game programmers say you should never provide access to data members through accessor member functions because even though this kind of access is indirect, it goes against the idea of encapsulation. Instead, they say you should write classes with member functions that provide the client with all of the functionality it could need, eliminating the client’s need to access a specific data member.

Q: What are mutable data members?

A: Data members that can be modified even by constant member functions. You create a mutable data member using the keyword `mutable`. You can also modify a mutable data member of a constant object.

Q: Why is it useful to have a default constructor?

A: Because there might be times when objects are automatically created without any argument values passed to a constructor—for example, when you create an array of objects.

Q: What is a structure?

A: A structure is very similar to a class. The only real difference is that the default access level for structures is public. You define a structure by using the keyword `struct`.