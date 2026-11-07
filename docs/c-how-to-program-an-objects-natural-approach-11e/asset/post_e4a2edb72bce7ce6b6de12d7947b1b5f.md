
## 12.12 Logging

One common task when handling exceptions is to log where they occurred into a human-readable text file that developers can analyze later for debugging purposes. Logging can be used during development time to help locate and fix problems. It also can be used once an application ships—if an application crashes, it might write a log file that the user can then send to the developer.

Logging is not built into the C++ standard library, though you could create your own logging mechanisms using C++’s file-processing capabilities. However, there are many open-source C++ logging libraries:

- Boost.Log—https://www.boost.org/doc/libs/1_75_0/libs/log/doc/html/
- Easylogging++—https://github.com/amrayn/easyloggingpp.
- Google Logging Library (glog)—https://github.com/google/glog.
- Loguru—https://github.com/emilk/loguru.
- Plog—https://github.com/SergiusTheBest/plog.
- spdlog—https://github.com/gabime/spdlog.

Some of these are header-only libraries that you can simply include in your projects. Others require installation procedures.

### Checkpoint

*(Fill-in)* Logging is built into the C++ standard library.

**Answer:** False. Actually, logging is not built into the C++ standard library, though you could create your own logging mechanisms using C++’s file-processing capabilities. There are many open-source C++ logging libraries.

## 12.13 Looking Ahead to Contracts⁴⁹

To strengthen your program’s error-handling architecture, you can specify the expected states before and after a function’s execution with preconditions and postconditions, respectively. We’ll define each, show precondition code examples and explain what happens when contracts are violated:

- A precondition⁵⁰ must be true when a function is invoked. Preconditions describe constraints on function parameters and any other expectations the function has just before it begins executing. If the preconditions are not met, then the function’s behavior is undefined—it may throw an exception, proceed with an illegal value or attempt to recover from the error. If code with undefined behavior is allowed to proceed, the results could be unpredictable and not portable across platforms. Each function can have multiple preconditions.
- A postcondition⁵¹ is true after the function successfully returns. Postconditions describe guarantees about the return value or side effects the function may have. When defining a function, you should document all postconditions so that others know what to expect when they call your function. You also should ensure that your function honors its postconditions if its preconditions are met. Each function can have multiple postconditions.

- 49. **Contracts are not yet a standard C++ feature.** The syntax we show here could change.
- 50. “Precondition.” Wikipedia. Wikimedia Foundation. Accessed April 18, 2023. https://en.wikipedia.org/wiki/Precondition.

### Precondition and Postcondition Violations

Today, precondition and postcondition violations often are dealt with by throwing exceptions. Consider array and vector function at, which receives an index into the container. For a precondition, function at requires that its index argument be greater than or equal to 0 and less than the container’s size. If the precondition is met, at’s postcondition states that the function will return the item at that index; otherwise, at throws an out_of_range exception. As a client of an array or vector, we trust that function at satisfies its postcondition, provided that we meet the precondition.

Preconditions and postconditions are assertions, so you can implement them with the assert preprocessor macro (Section 12.6.1) as program control enters or exits a function. Preprocessor macros are generally deprecated in C++. Until contracts become part of C++, you’ll continue using the assert macro or custom C++ code to express preconditions, assertions and postconditions.

### Invariants

An invariant is a condition that should always be true in your code—that is, a condition that never changes. Class invariants must be true for each object of a class. They generally are tied to an object’s lifecycle. Class invariants remain true from the time an object is constructed until it’s destructed. For example:

- Section 9.6’s Account class requires that its m_balance data member always be non-negative.
- Section 9.7’s Time class requires that its m_hour data member always have a value in the range 0 through 23, and its m_minute and m_second members always have values in the range 0 through 59.

These invariants ensure that objects of these classes always maintain valid state information throughout their lifetimes.

Functions also may contain invariants. For example, in a function that searches for a specified value in a vector<int>, the invariant is that if the value is in the vector, the value’s index must be greater than or equal to 0 and less than the vector’s size.

### Design By Contract

Design by contract (DbC)⁵²,⁵³,⁵⁴ is a software-design approach created by Bertrand Meyer in the 1980s and used in the design of his Eiffel programming language. Using this approach,

- a function expects client code to meet the function’s precondition(s),
- if the preconditions are true, the function guarantees its postcondition(s) will be true, and
- any invariants are maintained.

A proposal to add support for contract-based programming (commonly referred to as “contracts”) to the C++ standard was first proposed in 2012 and later rejected.⁵⁵ Another proposal was eventually accepted for inclusion in C++20 but removed⁵⁶ late in C++20’s development cycle due to “lingering design disagreements and concerns.”⁵⁷ So, contracts have been pushed to at least C++23.

### Gradually Moving to Contracts in the C++ Standard Library

Herb Sutter says, “In Java and .NET, some 90% of all exceptions are thrown for precondition violations.” He also says, “The programming world now broadly recognizes that programming bugs (e.g., out-of-bounds access, null dereference, and in general all pre/post/assert-condition violations) cause a corrupted state that cannot be recovered from programmatically, and so they should never be reported to the calling code as exceptions or error codes that code could somehow handle.”⁵⁸

**A key idea behind incorporating contracts is that many errors we currently deal with via exceptions can be located via preconditions and postconditions, then eliminated by fixing the code.**⁵⁹

- 52. Bertrand Meyer, *Object-Oriented Software Construction*. Prentice Hall, 1988.
- 53. Bertrand Meyer, *In Touch of Class: Learning to Program Well with Objects and Contracts*, xvii. Springer Berlin AN, 2016.
- 54. “Design by Contract.” Wikipedia. Wikimedia Foundation. Accessed April 18, 2023. https://en.wikipedia.org/wiki/Design_by_contract.
- 55. Nathan Meyers, “What Happened to C++20 Contracts?” August 5, 2019. Accessed April 18, 2023. https://www.reddit.com/r/cpp/comments/cm7ek/what_happened_to_c20_contracts/.
- 56. Meyers, “What Happened to C++20 Contracts?”
- 57. Herb Sutter, “Trip Report: Summer ISO C++ Standards Meeting (Cologne),” July 2019. Accessed April 18, 2023. https://herbsutter.com/2019/07/20/trip-report-summer-iso-c-standards-meeting-cologne/.
- 58. Herb Sutter, “Trip Report: Summer ISO C++ Standards Meeting (Rapperswil),” July 2018. Accessed April 18, 2023. https://herbsutter.com/2018/07/20/trip-report-summer-iso-c-standards-meeting-rapperswil/.
- 59. Glennan Carnie, “Contract Killing (in Modern C++),” September 18, 2019. Accessed April 18, 2023. https://blog.feabhas.com/2019/09/contract-killing-in-modern-c/.

![](img/7b5e2088e71c7f78681d4ddbcf104c06_746_0.png)

A goal of contracts is to make most functions **noexcept**, which might enable the compiler to perform additional optimizations. Sutter says, “Gradually switching precondition violations from exceptions to contracts promises to eventually remove a majority of all exceptions thrown by the standard library.”<sup>60,61</sup>

### Contracts Attributes

The contracts proposal<sup>63</sup> introduces three attributes of the form

```text
[[contractAttribute optionalLevel optionalIdentifier: condition]]
```

that you can use to specify preconditions, postconditions and assertions for your functions. The **optionalIdentifier** is one of the function’s local variables for use in postconditions, as you’ll see in Fig. 12.9. The contract attributes are

- **expects**—for specifying a function’s preconditions that are checked before the function’s body begins executing,
- **ensures**—for specifying a function’s postconditions that are checked just before the function returns and
- **assert**—for specifying assertions that are checked as they’re encountered throughout a function’s execution.

If you specify multiple preconditions and postconditions, they’re checked in their order of declaration.

### Contracts Levels

There are three contract levels:

- **default** specifies a contract with little runtime overhead compared to the function’s typical execution time. If a level is not specified, the compiler assumes **default**.
- **audit** specifies a contract with significant runtime overhead compared to the function’s typical execution time. Such contracts are intended primarily for use during program development.
- **axiom** specifies a contract meant to be enforced by static code checkers rather than at runtime.

![](img/7b5e2088e71c7f78681d4ddbcf104c06_746_1.png)

![](img/7b5e2088e71c7f78681d4ddbcf104c06_746_2.png)

- 60. Sutter, “Trip report: Summer ISO C++ standards meeting (Rapperswil).”
- 61. Sutter, “Trip report: Summer ISO C++ standards meeting (Rapperswil).”
- 62. To get a sense of the number of exceptions thrown by C++ and its libraries, we searched for the word “throws” in the final draft of the C++ standard document located at https://isocpp.org/files/papers/N4860.pdf. The document is over 1,800 pages—450 pages cover the language, 1,000+ cover the standard library, and the rest are appendices, bibliography, cross references and indexes. “Throws” appears 422 times—there were 92 occurrences of “throws nothing,” 13 occurrences of “throws nothing unless…” (indicating an exception that is thrown as a result of stack unwinding) and 329 occurrences of functions that throw exceptions. Many of these 329 cases are examples of where contracts will help eliminate the need to throw exceptions.
- 63. G. Dos Reis, J. D. Garcia, J. Lakos, A. Meredith, N. Meyers and B. Stroustrup, “Support for Contract Based Programming in C++,” June 8, 2018. Accessed April 18, 2023. http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2018/p0542r5.html.
