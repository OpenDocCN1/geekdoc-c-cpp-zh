This principle is called *Resource Acquisition Is Initialization* (RAII). In contrast, if we called `new` 738 times, partly in loops and branches, can we be sure that we have called `delete` exactly 738 times? We know that there are tools for this, but these are errors that are better prevented than fixed.20 Of course, the encapsulation idea is not idiot-proof, but it is much less work to get it right than sprinkling (raw) pointers all over our program. We will discuss RAII in more detail in Section 2.4.2.1.

19. It is safe to assume that there are many more objects than classes; otherwise there is something wrong with the entire program design.

20. In addition, a tool only shows that the current run had no errors, but this might be different with other input.

+   3. Use smart pointers, which we will introduce in the next section (§1.8.3).

Pointers serve two purposes:

+   1. Referring to objects

+   2. Managing dynamic memory

The problem with so-called Raw Pointers is that we have no notion whether a pointer is only referring to data or also in charge of releasing the memory when it is not needed any longer. To make this distinction explicit at the type level, we can use Smart Pointers.

# C++11 1.8.3 Smart Pointers

Three new smart-pointer types are introduced in C++11: `unique_ptr`, `shared_ptr`, and `weak_ptr`. The already-existing smart pointer from C++03 named `auto_ptr` is generally considered as a failed attempt on the way to `unique_ptr` since the language was not ready at the time. It was therefore removed in C++17. All smart pointers are defined in the header `<memory>`. If you cannot use C++11 features on your platform (e.g., in embedded programming), the smart pointers in Boost are a decent replacement.

# C++11 1.8.3.1 Unique Pointer