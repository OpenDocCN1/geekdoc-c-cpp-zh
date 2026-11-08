
```cpp
double** carrots{ new double*[rows] {} };
for (size_t i = 0; i < rows; ++i)
    carrots[i] = new double[columns] {};
...
for (size_t i = 0; i < rows; ++i)
    delete[] carrots[i];
delete[] carrots;
```

The carrots array is a dynamic array of double* pointers, each in turn containing the address of an array of double values. The latter arrays, representing the rows of the multidimensional array, are allocated in the free store as well, one by one, by the first for loop. Once you’re done with the array, you must deallocate its rows again, one by one, using a second loop, before disposing of the carrots array itself.

Given the amount of boilerplate code required to set up such a multidimensional array and again to tear it down, it’s highly recommended to encapsulate such functionality in a reusable class. We’ll leave that to you as an exercise, after learning all about creating your own class types in upcoming chapters.

> **Tip** The naïve technique we presented here to represent dynamic multidimensional arrays is not the most efficient one. It allocates all rows separately in the free store, meaning they are likely not contiguous in memory anymore. Programs tend to run much, much faster when operating on contiguous memory. That’s why classes that encapsulate multidimensional arrays generally allocate only a single array of rows * columns elements and then map array accesses at row i and column j to a single index using the formula i * columns + j.

## Member Selection Through a Pointer

A pointer can store the address of an object of a class type, such as a vector<T> container. Objects usually have member functions that operate on the object—you saw that the vector<T> container has an at() function for accessing elements and a push_back() function for adding an element, for example. Suppose pdata is a pointer to a vector<> container. This container could be allocated in the free store with a statement such as this:

```cpp
auto* pdata { new std::vector<int>{} };
```

But it might just as well be the address of a local object, obtained using the address-of operator.

```cpp
std::vector<int> data;
auto* pdata = &data;
```

In both cases, the compiler deduces the type of pdata to be vector<int>*, which is a “pointer to a vector of int elements.” For what follows, it does not matter whether the vector<int> is created in the free store or on the stack as a local object. To add an element, you call the push_back() function for the vector<int> object, and you have seen how you use a period between the variable representing the vector and the member function name. To access the vector object using the pointer, you could use the dereference operator, so the statement to add an element looks like this:

```cpp
(*pdata).push_back(66);        // Add an element containing 66
```

The parentheses around \*pdata are essential for the statement to compile because the . operator is of higher precedence than the \* operator. This clumsy-looking expression would occur very frequently when you are working with objects, which is why C++ provides an operator that combines dereferencing a pointer to an object and then selecting a member of the object. You can write the previous statement like this:

```cpp
pdata->push_back(66);       // Add an element containing 66
```

The -> operator is formed by a minus sign and a greater-than character and is referred to as the *arrow operator* or *indirect member selection operator*. The arrow is much more expressive of what is happening here. You'll be using this operator extensively later in the book.

## Hazards of Dynamic Memory Allocation

There are many kinds of serious problems you may run into when you allocate memory dynamically using new. In this section, we name the most common ones. Unfortunately, these hazards are all too real, as any developer who has worked with new and delete will corroborate. As a C++ developer, a significant portion of the more serious bugs you deal with often boil down to mismanagement of dynamic memory.

In this section, we will thus paint you a seemingly very bleak picture, filled with all kinds of hazards of dynamic memory. But don't despair. We will show you the way out of this treacherous minefield soon enough! Right after this section we will list the proven idioms and utilities that actually make it easy for you to avoid most if not all of these problems. In fact, you already know about one such utility: the std::vector<> container. This container is almost always the better choice over allocating dynamic memory directly using new[]. Other facilities of the Standard Library to better manage dynamic memory are discussed in upcoming sections. But first let's dwell on all these lovely risks, hazards, pitfalls, and other perils alike that are associated with dynamic memory.

### Dangling Pointers and Multiple Deallocations

A *dangling pointer*, as you know, is a pointer variable that still contains the address to free store memory that has already been deallocated by either *delete* or *delete[]*. Dereferencing a dangling pointer makes you read from or, often worse, write to memory that might already be allocated to and used by other parts of your program, resulting in all kinds of unpredictable and unexpected results. *Multiple deallocations*, which occur when you deallocate an already deallocated (and hence dangling) pointer for a second time using either *delete* or *delete[]*, is another recipe for disaster.

We taught you one basic strategy already to guard yourself against dangling pointers, that is, to always reset a pointer to nullptr after the memory it points to is released. In more complex programs, however, different parts of the code often collaborate by accessing the same memory—an object or an array of objects—all through distinct copies of the same pointer. In such cases our simple strategy rapidly falls short. Which part of the code is going to call delete/delete[]? And when? That is, how do you be sure that no other part of the code is still using the same dynamically allocated memory?

### Allocation/Deallocation Mismatch

A dynamically allocated array, allocated using new[], is captured in a regular pointer variable. But so is a single allocated value that is allocated using new:

```cpp
int* single_int{ new int{123} };      // Pointer to a single integer, initialized with 123
int* array_of_ints{ new int[123] };   // Pointer to an array of 123 uninitialized integers
```

After this, the compiler has no way to distinguish between the two, especially once such a pointer gets passed around different parts of the program. This means that the following two statements will compile without error (and in many cases even without a warning):

```cpp
delete[] single_int;    // wrong!
delete array_of_ints;   // wrong!
```

What'll happen if you mismatch your allocation and deallocation operators depends entirely on the implementation associated with your compiler. But it won't be anything good.

> **Caution** Every new must be paired with a single delete; every new[] must be paired with a single delete[]. Any other sequence of events leads to either undefined behavior or memory leaks (discussed next).

### Memory Leaks

A memory leak occurs when you allocate memory using new or new[] and fail to release it. If you lose the address of free store memory you have allocated, by overwriting the address in the pointer you were using to access it, for instance, you have a memory leak. This often occurs in a loop, and it's easier to create this kind of problem than you might think. The effect is that your program gradually consumes more and more of the free store, with the program potentially slowing more and more down, or even failing at the point when all of the free store has been allocated.

When it comes to scope, pointers are just like any other variable. The lifetime of a pointer extends from the point at which you define it in a block to the closing brace of the block. After that it no longer exists, so the address it contained is no longer accessible. If a pointer containing the address of a block of memory in the free store goes out of scope, then it's no longer possible to delete the memory.

It's still relatively easy to see where you've simply forgotten to use delete to free memory when use of the memory ceases at a point close to where you allocated it, but you'd be surprised how often programmers make mistakes like this, especially if, for instance, return statements creep in between the allocation and deallocation of your variable. And, naturally, memory leaks are even more difficult to spot in complex programs, where memory may be allocated in one part of a program and should be released in a completely separate part.

One basic strategy for avoiding memory leaks is to immediately add the delete operation at an appropriate place each time you use the new operator. But this strategy is by no means fail-safe. We cannot stress this enough: humans, even C++ programmers, are fallible creatures. So, whenever you manipulate dynamic memory directly, you will, sooner or later, introduce memory leaks. Even if it works at the time of writing, all too often bugs find their way into the program as it evolves further, return statements are added, conditional tests change, exceptions are thrown (see Chapter 16), and so on. And all of a sudden there are scenarios where your memory is no longer freed correctly!

### Fragmentation of the Free Store

Memory fragmentation can arise in programs that frequently allocate and release memory blocks. Each time the new operator is used, it allocates a contiguous block of bytes. If you create and destroy many memory blocks of different sizes, it's possible to arrive at a situation in which the allocated memory is interspersed with small blocks of free memory, none of which is large enough to accommodate a new memory allocation.
