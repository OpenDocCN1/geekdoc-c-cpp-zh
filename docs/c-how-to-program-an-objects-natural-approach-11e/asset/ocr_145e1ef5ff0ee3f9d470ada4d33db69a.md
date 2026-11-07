+   - discuss the storage classes and storage duration, which together determine an object's lifetime.
+   - introduce operator keywords for programmers with keyboards that do not support certain characters used in operator symbols, such as !, &, ^, and |.
+   - introduce the compile-time `decltype` operator to deduce types from expressions, typically used in template metaprogramming (Section 15.13).
+   - revisit trailing return types for functions (introduced in Section 14.3), typically used in more complex function-template definitions.
+   - use the `[[nodiscard]]` attribute to indicate that a function's return value should not be ignored, enabling compilers to warn you when the return value is not used in your program. We also show C++20's `[[nodiscard]]` enhancement, which includes a string that the compiler will display as the reason the function's caller should not ignore the return value.
+   - introduce some key C++23 features.

# ## 20.2 `shared_ptr` and `weak_ptr` Smart Pointers

Sections 11.4–11.5 introduced dynamic memory allocation and smart pointers. You learned that many common bugs in C++ code are related to pointers and dynamically allocated memory and that smart pointers help you avoid such errors by providing additional functionality that strengthens memory allocation and deallocation. Smart pointers also help you write exception-safe code (introduced in Section 12.3). If a program throws an exception before `delete` has been called on a pointer to dynamically allocated memory, a memory leak occurs. On the other hand, smart pointers use resource acquisition is initialization (RAII; Section 11.5). A smart pointer is an object, so when a smart pointer goes out of scope for any reason, including an exception, the smart pointer's destructor will still be called, helping avoid memory leaks. Section 11.5 introduced the `unique_ptr` class template. Here, we discuss `shared_ptr` and `weak_ptr`

# ### 20.2.1 Reference Counted `shared_ptr`

A `shared_ptr` (header `<memory>`) holds an internal pointer to a resource (e.g., a dynamically allocated object) that may be shared throughout a program. You can have many `shared_ptr`s to the same resource. As the type name implies, `shared_ptr`s share a resource—if you change the resource with one `shared_ptr`, the changes also will be “seen” by the other `shared_ptr`s. The internal pointer is deleted when the last `shared_ptr` to the resource is destroyed. Internally, `shared_ptr`s use reference counting to determine how many `shared_ptr`s point to the resource. Each time you create a new `shared_ptr` to a resource, the reference count increases, and each time one is destroyed, the reference count decreases. When the reference count reaches zero, the internal pointer is deleted, and the memory is released.

1. “std::shared_ptr.” Accessed April 18, 2023. https://en.cppreference.com/w/cpp/memory/shared_ptr.