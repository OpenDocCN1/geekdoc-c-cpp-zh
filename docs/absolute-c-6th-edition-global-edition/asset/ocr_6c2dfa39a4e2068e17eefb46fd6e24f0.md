If you have not already done so, you should read Section 7.3 of Chapter 7, which covers the vector template class of the STL. Although the current chapter does not use any of the material in Chapter 17, most readers will find that reading Chapter 17 before reading this one will aid his or her comprehension of this chapter by giving sample concrete implementations of some of the abstract ideas intrinsic to the STL. This chapter does not use any of the material in Chapters 12 to 15.

# 19.1 Iterators

> To iterate is human, and programmers are human.

ANONYMOUS

If you have not yet done so, you should read Chapter 10 on pointers and arrays and also read Section 7.3 of Chapter 7, which covers vectors. Vectors are one of the container template classes in the STL. Iterators are a generalization of pointers. This section shows how to use iterators with vectors. Other container template classes that we introduce in Section 19.2 use iterators in the same way. So, all that you learn about iterators in this section will apply across a wide range of containers rather than applying solely to vectors. This reflects one of the basic tenets of the STL philosophy: The semantics, naming, and syntax for iterator usage should be (and are) uniform across different container types.

# Iterator Basics

An iterator is a generalization of a pointer, and in fact is typically even implemented using a pointer, but the abstraction of an iterator is designed to spare you the details of the implementation and give you a uniform interface to iterators that is the same across different container classes. Each container class has its own iterator types, just like each data type has its own pointer type. But just as all pointer types behave essentially the same for dynamic variables of their particular data type, so too does each iterator type behave the same, but each iterator is used only with its own container type.

An iterator is not a pointer, but you will not go far wrong if you think of it and use it as if it were. Like a pointer variable, an iterator variable is located at (meaning, it points to) one data entry in the container. You manipulate iterators using the following overloaded operators that apply to iterator objects:

+   - Prefix and postfix increment operators (++) for advancing the iterator to the next data item.
+   - Prefix and postfix decrement operators (--) for moving the iterator to the previous data item.
+   - Equal and unequal operators (== and !=) to test whether two iterators point to the same data location.