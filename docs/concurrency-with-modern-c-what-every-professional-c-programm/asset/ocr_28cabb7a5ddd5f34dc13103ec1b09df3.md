![](bbox=[0.08, 0.13, 0.9, 0.34])

Memory Model in C++

# ## 2.1 Basics of the Memory Model

From the concurrency point of view, there are two main aspects of the memory model:

+   - What is a memory location?
+   - What happens if two threads access the same memory location?

Let me answer both questions.

# ### 2.1.1 What is a memory location?

A memory location is according cppreference.com¹

+   - an object of scalar type (arithmetic type, pointer type, enumeration type, or std::nullptr_t),
+   - or the largest contiguous sequence of bit fields of non-zero length.

Here is an example of a memory location:

¹http://en.cppreference.com/w/cpp/language/memory_model