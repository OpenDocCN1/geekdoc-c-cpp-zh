# 11. Structs

Structs are similar to classes in that they represent data structures that can contain data members and function members. However, unlike classes, structs are value types and do not require heap allocation. A variable of a struct type directly contains the data of the struct, whereas a variable of a class type contains a reference to the data, the latter known as an object.

> > **ERIC LIPPERT**  The statement that “structs do not require heap allocation” is not the statement “all instances of all structs are always allocated on the stack.” First, the second statement is not true: The memory for a DateTime field of a Customer class will be allocated on the heap along with the rest of the memory of the Customer class. Second, whether a local variable of value type is allocated by changing the stack register in the CPU is an implementation detail of a particular version of the framework. The specification is pointing out the opportunity for an optimization here, not stating that a particular allocation pattern is required.

Structs are particularly useful for small data structures that have value semantics. Complex numbers, points in a coordinate system, or key–value pairs in a dictionary are all good examples of structs. Key to these data structures is that they have few data members, that they do not require use of inheritance or referential identity, and that they can be conveniently implemented using value semantics where assignment copies the value instead of the reference.

As described in §4.1.4, the simple types provided by C#, such as int, double, and bool, are, in fact, all struct types. Just as these predefined types are structs, so it is also possible to use structs and operator overloading to implement new “primitive” types in the C# language. Two examples of such types are given at the end of this chapter (§11.4).

> > **BILL WAGNER**  All simple types are immutable. Any structs you create should also be immutable.