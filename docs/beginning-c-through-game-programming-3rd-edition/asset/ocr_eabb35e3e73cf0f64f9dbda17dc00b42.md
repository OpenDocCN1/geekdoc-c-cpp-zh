Q: Is a vector as fast as an array?

A: Accessing a vector element can be just as fast as accessing an array element. Also, iterating though a vector can be just as fast as iterating through an array.

Q: If I can use the subscripting operator with vectors, why would I ever need iterators?

A: There are several reasons. First, many of the vector member functions require iterators. (insert() and erase() are two examples.) Second, STL algorithms require iterators. And third, you can’t use the subscripting operator with most of the STL containers, so you’re going to have to learn to use iterators sooner or later.

Q: Which is the best way to access elements of a vector—through iterators or through the subscripting operator?

A: It depends. If you need random-element access, then the subscripting operator is a natural fit. If you need to use STL algorithms, then you must use iterators.

Q: What about iterating through the elements of a vector? Should I use the subscripting operator or an iterator?

A: You can use either method. However, an advantage of using an iterator is that it gives you the flexibility to substitute a different STL container in place of a vector (such as a list) without much code changing.

Q: Why does the STL define more than one sequential container type?

A: Different sequential container types have different performance properties. They’re like tools in a toolbox; each tool is best suited for a different job.

Q: What are container adaptors?

A: Container adaptors are based on one of the STL sequence containers; they represent standard computer data structures. Although they are not official containers, they look and feel just like them.

Q: What’s a stack?

A: A data structure in which elements are removed in the reverse order from how they were added. This means that the last element added is the first one