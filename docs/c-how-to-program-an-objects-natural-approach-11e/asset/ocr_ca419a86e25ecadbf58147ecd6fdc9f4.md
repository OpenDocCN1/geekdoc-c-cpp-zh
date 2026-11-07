# Algorithms

Standard library algorithms (which we’ll cover in Chapter 14) are function templates that perform common data manipulations, such as searching, sorting, copying, transforming and comparing elements or entire containers. The standard library provides over 100 algorithms:

+   - 90 in the `<algorithm>` header’s `std` namespace—82 also are overloaded in the `std::ranges` namespace for use with C++20 ranges.
+   - 11 in the `<numeric>` header’s `std` namespace,
+   - 14 in the `<memory>` header’s `std` namespace—all 14 also are overloaded in the `std::ranges` namespace for use with C++20 ranges and
+   - 2 in the `<cstdlib>` header.

For the complete list of algorithms with links to their descriptions, visit:

https://en.cppreference.com/w/cpp/algorithm

Most algorithms use iterators to access container elements. Each algorithm has minimum requirements for the kinds of iterators that can be used with it. We’ll see that containers support specific kinds of iterators, some more powerful than others. The iterators a container supports determine whether the container can be used with a specific algorithm. Iterators encapsulate the mechanisms used to traverse containers and access their elements, enabling many algorithms to be applied to containers with significantly different implementations. This also enables you to create new algorithms that can process the elements of multiple container types.

# C++20 Ranges

Chapter 6 introduced C++20’s ranges and views. You saw that a range is a collection of elements you can iterate over. So, arrays and vectors are ranges. You also used views to specify pipelines of operations that manipulate ranges of elements. Any container with iterators representing its beginning and end can be treated as a C++20 range. In this chapter, we’ll use the C++20 standard library algorithm `std::ranges::copy` and the older C++ standard library algorithm `std::copy` to demonstrate how ranges simplify your code. In Chapter 14, we’ll use many more C++20 algorithms from the `std::ranges` namespace to demonstrate additional ranges and views features.

# Custom Templatized Data Structures

Some popular data structures include linked lists, queues, stacks and binary trees:

+   - Linked lists are collections of data items logically “lined up in a row.” Insertions and removals are made anywhere in a linked list.
+   - **Stacks** are important in compilers and operating systems. Insertions and removals are made **only** at one end of a stack—its **top**.
+   - Queues represent waiting lines. Insertions are made at the back (also called the **tail**), and removals are made from the front (also called the **head**).
+   - Binary trees are nonlinear, hierarchical data structures that facilitate **searching** and **sorting** data and **duplicate elimination**.