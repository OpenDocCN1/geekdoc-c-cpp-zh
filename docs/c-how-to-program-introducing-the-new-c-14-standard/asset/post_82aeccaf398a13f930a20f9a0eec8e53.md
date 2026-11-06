
- C. Write a statement that returns a reference to the bit `bitNumber` of `bitset flags`.
- D. Write an expression that returns the number of bits that are set in `bitset flags`.
- E. Write an expression that returns `true` if all of the bits are set in `bitset flags`.
- F. Write an expression that compares `bitset flags` and `otherFlags` for inequality.
- G. Write an expression that shifts the bits in `bitset flags` left by `n` positions.

## Exercises

- 1. 15.4 State whether each of the following is **true** or **false**. If **false**, explain why.
  - A. Many of the Standard Library algorithms can be applied to various containers independently of the underlying container implementation.
  - B. `arrays` are fixed in size and offer direct access to any element.
  - C. `forward_lists` are singly linked lists, that offer rapid insertion and deletion only at the front and the back.
  - D. `sets` offer rapid lookup and duplicates are allowed.
  - E. In a `priority_queue`, the lowest-priority element is always the first element out.
  - F. The sequence containers represent non-linear data structures.
  - G. As of C++11, there is now a non-member function version of `swap` that swaps the contents of its two arguments (which must be of different container types) using move operations rather than copy operations.
  - H. Container member function `erase` removes all elements from the container.
  - I. An object of type `iterator` refers to a container element that can be modified.
  - J. We use `const` versions of the iterators for traversing read-only containers.
  - K. For input iterators and output iterators, it’s common to save the iterator, then use the saved value later.
  - L. Class templates `array`, `vector` and `deque` are based on built-in arrays.
  - M. Attempting to dereference an iterator positioned outside its container is a compilation error. In particular, the iterator returned by `end` should not be dereferenced or incremented.
  - N. Insertions and deletions in the middle of a `deque` are optimized to minimize the number of elements copied, so it’s more efficient than a `vector` but less efficient than a `list` for this kind of modification.
  - O. Container `set` does *not* allow duplicates.
  - P. Class `stack` (from header `<stack>`) enables insertions into and deletions from the underlying data structure at one end (commonly referred to as a last-in, first-out data structure).
  - Q. Function `empty` is available in all containers except the `deque`.

- 2. 15.5 Fill in the blanks in each of the following statements:
  - A. The three styles of container classes are first-class containers, ______ and near containers.
  - B. Containers are divided into four major categories—sequence containers, ordered associative containers, and container adapters.
  - C. The Standard Library container adapter most closely associated with the first-in, first-out (FIFO) insertion-and-removal discipline is the _____.
  - D. Built-in arrays, `bitsets` and `valarrays` are all _____ containers.
  - E. A(n) _____ constructor (C++11) moves the contents of an existing container of the same type into a new container, without the overhead of copying each element of the argument container.
  - F. The _____ container member function returns the number of elements currently in the container.
  - G. The _____ container member function returns `true` if the contents of the first container are not equal to the contents of the second; otherwise, returns `false`.
  - H. We use iterators with sequences—these can be input sequences or output sequences, or they can be _____ .
  - I. The Standard Library algorithms operate on container elements indirectly via _____ .
  - J. Applications with frequent insertions and deletions in the middle and/or at the extremes of a container normally use a(n) _____ .
  - K. Function _____ is available in *every* first-class container (except `forward_list`) and it returns the number of elements currently stored in the container.
  - L. It can be wasteful to double a `vector`’s size when more space is needed. For example, a full `vector` of 1,000,000 elements resizes to accommodate 2,000,000 elements when a new element is added, leaving 999,999 unused elements. You can use `reserve` and `shrink_to_fit` to control space usage better.
  - M. As of C++11, you can ask a `vector` or `deque` to return unneeded memory to the system by calling member function `shrink_to_fit`.
  - N. The associative containers provide direct access to store and retrieve elements via keys (often called search keys). The ordered associative containers are `multiset`, `set`, `map`, and `multimap`.
  - O. Classes `set` and `multiset` provide operations for manipulating sets of values where the values are the keys—there is *not* a separate value associated with each key.
  - P. We use C++11’s `auto` keyword to deduce the type of a variable from its initializer.
  - Q. A `multimap` is implemented to efficiently locate all values paired with a given key.
  - R. The Standard Library container adapters are `stack`, `queue` and `priority_queue`.

### Discussion Questions

- 1. 15.6 Why is it expensive to insert (or delete) an element in the middle of a `vector`?
- 2. **15.7** Containers that support random-access iterators can be used with most but not all Standard Library algorithms. What is the exception?
- 3. **15.8** Why would you use operator `*` to dereference an iterator?
- 4. **15.9** Why is insertion at the back of a `vector` efficient?
- 5. **15.10** When would you use a `deque` in preference to a `vector`?
- 6. **15.11** Describe what happens when you insert an element in a vector whose memory is exhausted.
- 7. **15.12** When would you prefer a `list` to a `deque`?
- 8. **15.13** What happens when the map subscript is a key that’s not in the map?
- 9. **15.14** Use C++11 list initializers to initialize the `vector` `names` with the `string`s "Suzanne", "James", "Maria" and "Juan". Show both common syntaxes.
- 10. **15.15** What happens when you erase a container element that contains a pointer to a dynamically allocated object?
- 11. **15.16** Describe the multiset ordered associative container.
- 12. **15.17** How might a `multimap` ordered associative container be used in a credit-card transaction processing system?
- 13. **15.18** Write a statement that creates and initializes a multimap of strings and ints with three key–value pairs.
- 14. **15.19** Explain the `push`, `pop` and `top` operations of a `stack`.
- 15. **15.20** Explain the `push`, `pop`, `front` and `back` operations of a `queue`.
- 16. **15.21** How does inserting an item in a `priority_queue` differ from inserting an item in virtually any other container?

### Programming Exercises

- 1. 15.22 **_Palindromes_** Write a function template `palindrome` that takes a `vector` parameter and returns `true` or `false` according to whether the `vector` does or does not read the same forward as backward (e.g., a `vector` containing 1, 2, 3, 2, 1 is a palindrome, but a `vector` containing 1, 2, 3, 4 is not).
- 2. 15.23 **_Sieve of Eratosthenes with `bitset`_** This exercise revisits the *Sieve of Eratosthenes* for finding prime numbers that we discussed in [Exercise 7.27](#). Use a `bitset` to implement the algorithm. Your program should display all the prime numbers from 2 to 1023, then allow the user to enter a number to determine whether that number is prime.
- 3. 15.24 **_Sieve of Eratosthenes_** Modify [Exercise 15.23](#), the Sieve of Eratosthenes, so that, if the number the user inputs into the program is not prime, the program displays the prime factors of the number. Remember that a prime number’s factors are only 1 and the prime number itself. Every nonprime number has a unique prime factorization. For example, the factors of 54 are 2, 3, 3 and 3. When these values are multiplied together, the result is 54. For the number 54, the prime factors output should be 2 and 3.
- 4. 15.25 **_Prime Factors_** Modify [Exercise 15.24](#) so that, if the number the user inputs into the program is not prime, the program displays the prime factors of the number and the number of times each prime factor appears in the unique prime
