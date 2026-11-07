# ## 14.2 **Algorithm Requirements: C++20 Concepts**

The C++ standard library separates containers from the algorithms that manipulate the containers. Most algorithms operate on container elements indirectly via iterators. **This architecture makes it easier to write generic algorithms applicable various containers**—a strength of the standard library algorithms.

Container class templates and their corresponding iterator class templates typically reside in the same header. For example, the `<vector>` header contains the templates for vector and its iterator class. A container internally creates objects of its iterator class and returns them via container member functions, such as begin, end, cbegin and cend.

# ### Iterator Requirements

For maximum reuse, **each algorithm can operate on any container that meets the algorithm’s minimum iterator requirements.**⁴ For example, an algorithm requiring forward iterators can operate on any container that provides **at least forward iterators.** All standard library algorithms can operate on **vectors and arrays** because they support contiguous iterators that provide every iterator operation discussed in Section 13.5.

Before C++20,

+   - each container’s documentation mentioned the iterator level it supported, and
+   - each algorithm’s documentation mentioned its minimum iterator requirements.

You were expected to adhere to an algorithm’s documented requirements by using only containers with iterators that satisfied those requirements. If you passed the wrong iterator type, the compiler would substitute that type throughout the algorithm’s template definition and, as Bjarne Stroustrup observed, produce “spectacularly bad error messages.”⁵

# ### C++20 Concepts

One of the “big four” C++20 features is **concepts**—a technology for constraining the types used with templates. Stroustrup points out that “Concepts complete C++ templates as originally envisioned”⁶ decades ago. Each concept specifies a type’s requirements or a relationship between types.⁷

When an algorithm’s parameter is constrained by a concept, the compiler can check the requirements in the function call before substituting the argument’s type throughout the function template. If your argument’s type does not satisfy the concept’s requirements, a benefit of concepts is that the compiler produces many fewer and much clearer error messages than for the older common-range algorithms. This makes it easier for you to understand the errors and correct your code.

This chapter’s primary focus is C++20’s new range-based algorithms, which are **constrained with many C++20 predefined concepts.** There are 76 predefined concepts in the

4. Alexander Stepanov and Meng Lee, “The Standard Template Library, Section 2: Structure of the Library,” October 31, 1995. Accessed April 18, 2023. http://stepanovpapers.com/SLT/DOC.PDF.

5. Bjarne Stroustrup, “Concepts: The Future of Generic Programming—1. A Bit of Background,” January 31, 2017. Accessed April 18, 2023. http://wg21.link/p0557r0.

6. Bjarne Stroustrup, “Concepts: The Future of Generic Programming—Conclusion,” January 31, 2017. Accessed April 18, 2023. http://wg21.link/p0557r0.

7. Bjarne Stroustrup, “Concepts: The Future of Generic Programming—3.1 Specifying Template Interfaces,” January 31, 2017. Accessed April 18, 2023. http://wg21.link/p0557r0.