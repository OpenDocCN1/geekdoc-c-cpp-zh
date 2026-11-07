# 3.1 exposition-only concepts (Cont.)

|  |  |
|---|---|
| **Comparisons in the language support library** |  |
| `compares-as` | `partially-ordered-with` |
| **Memory library** |  |
| `no-throw-forward-iterator` | `no-throw-input-iterator` · `no-throw-sentinel` |
| `no-throw-forward-range` | `no-throw-input-range` |

# 15.6.7 Techniques Before C++20 Concepts: SFINAE and Tag Dispatch

With each new C++ standard, metaprogramming gets more powerful and convenient. There’s a history of several technologies that led to C++20 Concepts, including SFINAE, tag dispatch and constexpr if (Section 15.13.3 shows constexpr). For an overview of the progression through these technologies, see the blog post, “Notes on C++ SFINAE, Modern C++ and C++20 Concepts.”⁶³

# SFINAE—Substitution Failure Is Not an Error

Earlier, we mentioned that when you call a function, the compiler locates all the functions that might satisfy the function call—known as the overload set. From these overloads, the compiler chooses the best match. This process often includes instantiating function templates based on a function call’s argument types.

Before concepts, developers had to be significantly more familiar with template specialization rules. Since template debugging is nontrivial, this made the code more error-prone. Template metaprogramming techniques involving `std::enable_if` were commonly used with type traits to check if a function-template argument satisfied a template’s requirements. If not, the compiler would generate invalid code. It would then ignore that code, removing it from the overload set. SFINAE (substitution failure is not an error)⁶⁴,⁶⁵,⁶⁶ describes how the compiler discards invalid template code as it determines the correct function to call. SFINAE prevents the compiler from immediately generating potentially lengthy lists of errors when first instantiating a template. The compiler generates error messages only if it cannot find a match for the function call in the overload set.

# Tag Dispatch

Using the tag-dispatch⁶⁷ technique, you can tell the compiler the version of an overloaded function to call based on template type parameters and properties of those types. Bjarne Stroustrup—in his paper “Concepts: The Future of Generic Programming”—refers to

63. Bartlomiej Filipek, “Notes on C++ SFINAE, Modern C++ and C++20 Concepts,” April 20, 2020. Accessed April 18, 2023. https://www.bfilipek.com/2016/02/notes-on-c-sfinae.html.

64. “SubstitutionFailure Is Not an Error.” Wikipedia, Wikimedia Foundation. Accessed April 18, 2023. https://en.wikipedia.org/wiki/Substitution_failure_is_not_an_error.

65. Filipek, “Notes on C++ SFINAE, Modern C++ and C++20 Concepts.”

66. David Vandevoorde and Nicolai M. Josuttis, C++ Templates: The Complete Guide. Addison-Wesley Professional, 2002.

67. “Generic Programming—Tag Dispatching.” Accessed April 18, 2023. https://www.boost.org/community/generic_programming.html#tag_dispatching.