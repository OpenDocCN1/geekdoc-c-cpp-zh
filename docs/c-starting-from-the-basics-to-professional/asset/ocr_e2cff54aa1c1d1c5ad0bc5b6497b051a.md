The parentheses around \*pdata are essential for the statement to compile because the . operator is of higher precedence than the \* operator. This clumsy-looking expression would occur very frequently when you are working with objects, which is why C++ provides an operator that combines dereferencing a pointer to an object and then selecting a member of the object. You can write the previous statement like this:

```
pdata->push_back(66);       // Add an element containing 66
```

The -> operator is formed by a minus sign and a greater-than character and is referred to as the *arrow operator* or *indirect member selection operator*. The arrow is much more expressive of what is happening here. You'll be using this operator extensively later in the book.

# Hazards of Dynamic Memory Allocation

There are many kinds of serious problems you may run into when you allocate memory dynamically using new. In this section, we name the most common ones. Unfortunately, these hazards are all too real, as any developer who has worked with new and delete will corroborate. As a C++ developer, a significant portion of the more serious bugs you deal with often boil down to mismanagement of dynamic memory.

In this section, we will thus paint you a seemingly very bleak picture, filled with all kinds of hazards of dynamic memory. But don't despair. We will show you the way out of this treacherous minefield soon enough! Right after this section we will list the proven idioms and utilities that actually make it easy for you to avoid most if not all of these problems. In fact, you already know about one such utility: the std::vector<> container. This container is almost always the better choice over allocating dynamic memory directly using new[]. Other facilities of the Standard Library to better manage dynamic memory are discussed in upcoming sections. But first let's dwell on all these lovely risks, hazards, pitfalls, and other perils alike that are associated with dynamic memory.

# Dangling Pointers and Multiple Deallocations

A *dangling pointer*, as you know, is a pointer variable that still contains the address to free store memory that has already been deallocated by either *delete* or *delete[]*. Dereferencing a dangling pointer makes you read from or, often worse, write to memory that might already be allocated to and used by other parts of your program, resulting in all kinds of unpredictable and unexpected results. *Multiple deallocations*, which occur when you deallocate an already deallocated (and hence dangling) pointer for a second time using either *delete* or *delete[]*, is another recipe for disaster.

We taught you one basic strategy already to guard yourself against dangling pointers, that is, to always reset a pointer to nullptr after the memory it points to is released. In more complex programs, however, different parts of the code often collaborate by accessing the same memory—an object or an array of objects—all through distinct copies of the same pointer. In such cases our simple strategy rapidly falls short. Which part of the code is going to call delete/delete[]? And when? That is, how do you be sure that no other part of the code is still using the same dynamically allocated memory?

# Allocation/Deallocation Mismatch

A dynamically allocated array, allocated using new[], is captured in a regular pointer variable. But so is a single allocated value that is allocated using new:

```
int* single_int{ new int{123} };      // Pointer to a single integer, initialized with 123
int* array_of_ints{ new int[123] };   // Pointer to an array of 123 uninitialized integers
```