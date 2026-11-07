
**Chapter 11, Operator Overloading, Copy/Move Semantics and Smart Pointers**, shows how to enable C++’s existing operators to work with custom class objects and introduces smart pointers and dynamic memory management. Smart pointers help you avoid dynamic memory management errors and “resource leaks” by providing additional functionality beyond that of built-in pointers. We discuss `unique_ptr` in this chapter and `shared_ptr` and `weak_ptr` in Chapter 20, Other Topics and a Look Toward the Future of C++.

A key aspect of Chapter 11 is crafting valuable classes. We begin with a string class test-drive, presenting an elegant use of operator overloading before you implement your own customized class with overloaded operators. Then, in our **Crafting Valuable Classes case study—one of the book’s most important examples**—you’ll build your own custom MyArray class using overloaded operators and other capabilities to solve various problems with C++’s native pointer-based arrays.¹² We introduce and implement the five special member functions you can define in each class—the copy constructor, copy assignment operator, move constructor, move assignment operator and destructor. We discuss copy semantics and move semantics, which enable a compiler to move resources from one object to another to avoid costly, unnecessary copies. We introduce C++20’s three-way comparison operator (`<=>`; also called the “spaceship operator”) and show how to implement custom conversion operators. In Chapter 15, you’ll convert a portion of the MyArray class into a class template that can store elements of a specified type. You will then have truly “crafted valuable classes.”

¹² In industrial-strength systems, you’ll use standard library classes for this, but this example enables us to go “under the hood” to demonstrate many modern C++ concepts.

**Chapter 12, Exceptions and a Look Forward to Contracts**, continues our exception-handling discussion that began in Chapter 6. We’ve enhanced Chapter 12’s coverage with discussions of when to use exceptions, exception safety guarantees, and using exceptions in the context of constructors and destructors. We show how to handle dynamic memory allocation failures. We discuss why some libraries provide dual interfaces, enabling developers to choose whether to use versions of functions that throw exceptions or versions that set error codes. The chapter concludes with a case study that introduces contracts—a possible C++26 feature. **One goal of contracts is to make most functions noexcept—meaning they do not throw exceptions—which might enable the compiler to perform additional optimizations and eliminate the overhead and complexity of exception handling. Another goal is to find errors faster, eliminate them during development and, hopefully, create more robust code for deployment.** We introduce preconditions, postconditions and assertions, and we discuss how they can be implemented as contracts that are tested at execution time. We demonstrate the example code using GCC’s experimental contracts implementation on https://godbolt.org.

## Part 4: Standard Library Containers, Iterators and Algorithms

**Chapter 13, Standard Library Containers and Iterators**, begins our broader and deeper treatment of three key C++ standard library components:

- containers (templatized data structures),
- iterators (for traversing containers and accessing their elements) and
- algorithms (which use iterators to manipulate containers).

A feature of this chapter is the **Crafting Valuable Classes case study**—you’ll reimplement Chapter 11’s **MyArray case study** as a class template with custom iterators that enable most C++ standard library algorithms to manipulate MyArray objects. We also define a custom algorithm that can process MyArray elements and standard library container class objects. We show that you can use concepts to overload functions based on the type requirements of their parameters. Finally, we introduce template metaprogramming for performing compile-time calculations, enabling you to improve a program’s execution-time performance, possibly reducing both execution time and memory consumption.

**Chapter 16, C++20 Modules**, presents another of C++20’s “big four” features. Modules provide a new way to organize your code, precisely control which declarations you expose to client code and encapsulate implementation details. Modules help you be more productive, especially when building, maintaining and evolving large software systems. Modules help such systems build faster and make them more scalable. C++ creator Bjarne Stroustrup says, “*Modules offer a historic opportunity to improve code hygiene and compile times for C++ (bringing C++ into the 21st century).*”¹³ You’ll see that, even in small systems, modules offer immediate benefits in every program by eliminating the need for the C++ preprocessor. In several **Software Engineering case studies**, you’ll learn several ways to **separate interface from implementation using modules**.

¹³ Bjarne Stroustrup, “Modules and Macros.” February 11, 2018. Accessed March 8, 2023. http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2018/p0955r0.pdf.

**Chapter 17, Parallel Algorithms and Concurrency: A High-Level View**, is the first of two extensive chapters on concurrency and multi-core programming. Chapter 17 is one of the most important chapters in the book, presenting C++’s features for building applications that create and manage multiple tasks. These can significantly improve program performance and responsiveness on today’s multi-core processors.

This chapter presents several **multithreading and multicore systems performance case studies**. In the **Profiling Sequential and Parallel Sorting Algorithms case study**, we show how to use prepackaged parallel algorithms to create multithreaded programs that will run faster (often much faster) on today’s multi-core computer architectures. For example, we sort 100 million values using a sequential sort, then a parallel sort. **We use timing operations from C++’s `<chrono>` library features to profile the performance improvement we get on today’s popular multi-core systems, as we employ more cores. You’ll see that the parallel sort runs 6.76 times faster than the sequential sort on our computer with an 8-core Intel processor.**

In the **Producer–Consumer: Synchronizing Access to Shared Mutable Data case studies**, we discuss the producer–consumer relationship and demonstrate various ways to implement it using low-level and high-level C++ concurrency primitives. We also present several **Coordinating Threads case studies using C++20’s new latch, barrier and semaphore capabilities**. We emphasize that concurrent programming is difficult to get right, so you should prefer the easier-to-use, higher-level concurrency features. Lower-level features like semaphores and atomics can be used to implement higher-level features like latches.

**Chapter 18, C++20 Coroutines**, is the second of our chapters on concurrency and multicore programming. This chapter presents coroutines—the last of C++20’s “big four” features. **A coroutine is a function that can suspend its execution and be resumed later, enabling you to do concurrent programming with a simple sequential-like coding style.** The mechanisms supporting this are handled entirely by code that's written for you by the compiler. A function containing any of the keywords `co_await`, `co_yield` or `co_return` is a coroutine.

![](img/7b5e2088e71c7f78681d4ddbcf104c06_35_0.png)

Coroutines require sophisticated infrastructure, which you can write yourself, but doing so is complex, tedious and error-prone. Instead, most experts agree that you should use high-level coroutine support libraries, which is the approach we show. The open-source community has created several experimental libraries for developing coroutines quickly and conveniently—we use two in our presentation. C++23 has standard library support for generator coroutines, and more coroutine support is expected in C++26.

We present three **multithreading and multicore systems performance case studies:**

- Creating a Generator Coroutine with `co_yield` and the generator Library
- Launching Tasks with `concurrencpp`
- Creating a Coroutine with `co_await` and `co_return`

To help readers understand how coroutines work, the first and third case studies include diagrams illustrating each application's flow of control.

**Chapter 19, Stream I/O & C++20 Text Formatting**, discusses C++ stream input/output capabilities and formatting features. We include stream formatting primarily for people who might encounter it in legacy code. Section 19.9 presents an in-depth case study on C++20’s new text-formatting features. In introductory computer science courses, instructors may wish to present Section 19.9 after we introduce C++20 text formatting in Chapter 4.

**Chapter 20, Other Topics and a Look Toward the Future of C++**, continues our discussion of runtime polymorphism from Chapter 10 with case studies on runtime type information (RTTI), inheriting base-class constructors, the non-virtual interface idiom, duck typing with `std::variant` and `std::visit` (for runtime polymorphism with objects of classes that are not related by inheritance), and multiple inheritance. The chapter also presents miscellaneous C++ topics, including storage classes, storage duration, mutable class members, namespaces, operator keywords, pointers to class members, the `[[nodiscard]]` attribute, the `std::shared_ptr` and `std::weak_ptr` smart pointers, determining types at compile-time with `decltype`, and the `[[likely]]` and `[[unlikely]]` attributes. The chapter ends with a look forward to features coming in the C++23 and C++26 standards.

**Chapter 21, Computer Science Thinking: Searching, Sorting and Big O**, introduces some classic computer-science topics. We consider several algorithms and compare their processor demands and memory consumption. We present a friendly introduction to computer science’s Big O notation, which indicates how hard an algorithm may have to work to solve a problem based on the number of items it must process.

The chapter includes two case studies that visualize the **high-speed binary search** and **merge sort algorithms** to illustrate how these algorithms work. In introductory computer science courses, instructors can present this chapter after Chapter 6.

## Modern C++ Data Structures Courses

Our recursion (Chapter 5), arrays (Chapter 6), searching (Chapters 6 and 21), sorting (Chapters 6 and 21), Big O (Chapter 21), containers (Chapter 13), iterators (Chapter 13)

![](img/7b5e2088e71c7f78681d4ddbcf104c06_36_0.png)

![](img/7b5e2088e71c7f78681d4ddbcf104c06_36_1.png)

![](img/7b5e2088e71c7f78681d4ddbcf104c06_36_2.png)
