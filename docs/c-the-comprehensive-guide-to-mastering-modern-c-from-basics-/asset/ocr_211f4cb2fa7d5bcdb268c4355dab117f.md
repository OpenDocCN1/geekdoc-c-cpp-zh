the 15p-unittest-100 project in the download sources, which defines an impl_simple_map namespace with an index_impl class contained within it. This is a different, simpler version of an index implementation.

In principle, you could run both namespaces in parallel and easily switch the implementation in the main class. However, this is just a suggestion here, which is why I only show it in a rudimentary way. If fully developed, this switchability would involve a bit more programming effort and is not the focus of this chapter.

Now follows the actual main class of the class index library. At its core, it contains a pimpl field of the index_impl class (as a pointer). With this “trick,” implementation details of the index interface class can be separated even better. Sometimes this is called the pointer to implementation (or Pimpl) pattern.

To avoid bothering users of the class with implementation details (or to keep them secret), all methods of the class are declared only. They are defined later in the quell.cpp implementation file.

Normally, as you will see in Chapter 17, you would not define a destructor, copy constructor, move constructor, assignment operator, or move operator (the “big five”). The compiler would generate them optimally for you. Unfortunately, that is not possible here: the compiler would need the definition of the index_impl class for this, because how else would it know what to do with