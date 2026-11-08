Naturally you can do more with an iterator than access the first element of the container. As you'll recall from Chapter 6, pointers support the arithmetic operations `++`, `--`, `+`, `-`, and `+=`, `-=`, which you could use to move from one element in an array to the next (or previous). You work with `vector<>` iterators in precisely the same manner. Here's an example:

```
```cpp
++my_iter;                         // Move my_iter to the next element
std::cout << *my_iter << std::endl; // b

my_iter += 2;                       // Move my_iter two elements further
std::cout << *my_iter-- << std::endl; // d
std::cout << *my_iter << std::endl;   // c (iterator altered using the post-decrement
                                      // operator in the previous statement)

auto copy( my_iter );               // Create a copy of my_iter (pointing at c)
my_iter += 2;                       // Move my_iter two elements further
std::cout << *copy << std::endl;    // c (copy not affected by moving my_iter)
std::cout << *my_iter << std::endl; // e
std::cout << my_iter - copy << std::endl; // 2
```
```

This code, which you can find in its entirety in Ex20_06, should really explain itself at this point, as all this is completely analogous to working with pointers. This even applies to the last line in our example, which is perhaps a bit less obvious than the others. That is, subtracting two `vector` iterators results in a value of a signed integer type that reflects the distance between the two iterators.

> **Tip** Iterators also provide a member access operator (informally, arrow operator), `->`, to access the member variables or functions of the element they refer to. That is, suppose `string_iter` is an iterator that refers to an element of type `std::string`; then `string_iter->length()` is short for `(*string_iter).length()`—again just like it is with a pointer. We will see more concrete examples later in the chapter.

# Different Flavors of Iterators

The iterator that we used for the example in the previous subsection is a so-called random-access iterator. Out of all iterator categories, random-access iterators offer the richest set of operations. All iterators returned by standard containers support operators `+`, `+`, and `-`, as well as `==` and `!=`. But beyond that, there are some differences. Any and all limitations are easily explained from the nature of the data structures behind the various containers:

+   - The iterators for a `std::forward_list<>` do not support `--`, `--`, or `-`. The reason, of course, is that there is no efficient way for an iterator to go back to the previous element. Each node in a singly-linked list only has a pointer to the next element in the list. Such iterators are referred to as *forward iterators*. Other containers that may only support forward iterators are the unordered associative containers.
+   
+   - The iterators for a `std::list<>`, on the other hand, do support the `--` decrement operators (both pre- and post-decrement). Going back to the previous node in a doubly-linked list is trivial. Jumping multiple elements at once still cannot be done efficiently, though. To discourage such use, `std::list<>` iterators do not feature, for instance, the `+=`, `-=`, `+`, or `-` operators. The iterators for the ordered associative containers have the same limitations, as traversing the nodes of the underlying tree data structure is similar to traversing those of a doubly-linked list. This category of iterators is termed *bidirectional iterators*—for obvious reasons.