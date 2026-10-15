ject contains the reference and allows the algorithm to use it as a value. Using references instead of values improves performance when passing large objects to an algorithm.

# Regex⁸

**Boost.Regex** provides support for processing regular expressions in C++. Regular expressions are used to match specific character patterns in text. Many modern programming languages have built-in support for regular expressions, but C++ does not. With Boost.Regex, you can search for a particular expression in a string, replace parts of a string that match a regular expression, and split a string into tokens using regular expressions to define the delimiters. These techniques are commonly used for text processing, parsing and input validation. We discuss the Boost.Regex library in more detail in Section 21.7.

# Result_of⁹

The class template **result_of** can be used to specify the return type of a call expression—that is, an expression that calls a function or calls the overloaded parentheses operator of a function object. The call expression’s return type is determined based on the types of the arguments passed to the call expression. This can be helpful in templatizing the return types of functions and function objects.

# Smart_ptr¹⁰

**Boost.Smart_ptr** defines smart pointers that help you manage dynamically allocated resources (e.g., memory, files and database connections). Programmers often get confused about when to deallocate memory or simply forget to do it, especially when the memory is referenced by more than one pointer. Smart pointers take care of these tasks automatically. TR1 includes two smart pointers from the Boost.Smart_ptr library. **shared_ptrs** handle lifetime management of dynamically allocated objects. The memory is released when there are no shared_ptrs referencing it. **weak_ptrs** allow you to observe the value held by a shared_ptr without assuming any management responsibilities. We discuss the Boost.Smart_ptr library in more detail in Section 21.8.

# Tuple¹¹

A tuple is a set of objects. **Boost.Tuple** allows you to create sets of objects in a generic way and allows generic functions to act on those sets. The library allows you to create tuples of up to 10 objects; that limit can be extended. Boost.Tuple is basically an extension to the STL’s std::pair class template. Tuples are often used to return multiple values from a function. They can also be used to store sets of elements in an STL container where each set of elements is an element of the container. Another useful feature is the ability to set the values of variables using the elements of a tuple.

8. Documentation for Boost.Regex, John Maddock, www.boost.org/libs/regex/doc/index.html.
9. Documentation for Boost.Result_of, Doug Gregor, www.boost.org/libs/utility/utility.htm#result_of.
10. Documentation for Boost.Smart_ptr, Greg Colvin and Beman Dawes, www.boost.org/libs/smart_ptr/smart_ptr.htm.
11. Documentation for Boost.Tuple, Jaakko Järvi, www.boost.org/libs/tuple/doc/tuple_users_guide.html.