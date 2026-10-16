representations of their operand class. Consequently, binary operators are the most common source of friend functions.

Unless type conversions are defined, there appears to be no compelling reason to choose a member over a friend taking a reference argument, or vice versa. In some cases, the programmer may have a preference for one call syntax over another. For example, most people seem to prefer the notation m2=inv(m) for producing a inverted Matrix from m to the alternative m2=m.inv(). On the other hand, if inv() inverts m itself, rather than producing a new Matrix that is the inverse of m, it should be a member.

All other things considered equal, implement operations that need direct access to a representation as member functions:

+   - It is not possible to know if someone someday will define a conversion operator.
+   - The member function call syntax makes it clear to the user that the object may be modified; a reference argument is far less obvious.
+   - Expressions in the body of a member can be noticeably shorter than the equivalent expressions in a global function; a nonmember function must use an explicit argument, whereas the member can use this implicitly.
+   - Member names are local to a class, so they tend to be shorter than the names of nonmember functions.
+   - If we have defined a member f() and we later feel the need for a nonmember f(x), we can simply define it to mean x.f().

Conversely, operations that do not need direct access to a representation are often best represented as nonmember functions, possibly in a namespace that makes their relationship with the class explicit (§18.3.6).

# 19.5 Advice

+   [1] Use operator[]( ) for subscripting and for selection based on a single value; §19.2.1.
+   [2] Use operator()( ) for call semantics, for subscripting, and for selection based on multiple values; §19.2.2.
+   [3] Use operator->( ) to dereference “smart pointers”; §19.2.3.
+   [4] Prefer prefix ++ over suffix ++; §19.2.4.
+   [5] Define the global operator new( ) and operator delete( ) only if you really have to; §19.2.5.
+   [6] Define member operator new( ) and member operator delete( ) to control allocation and deallocation of objects of a specific class or hierarchy of classes; §19.2.5.
+   [7] Use user-defined literals to mimic conventional notation; §19.2.6.
+   [8] Place literal operators in separate namespaces to allow selective use; §19.2.6.
+   [9] For nonspecialized uses, prefer the standard string (Chapter 36) to the result of your own exercises; §19.3.
+   [10] Use a friend function if you need a nonmember function to have access to the representation of a class (e.g., to improve notation or to access the representation of two classes); §19.4.
+   [11] Prefer member functions to friend functions for granting access to the implementation of a class; §19.4.2.

+   - Introduction