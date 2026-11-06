![](bbox=[0.05, 0.123, 0.131, 0.296])

+   **22.1** Introduction to the Standard Template Library (STL)
+   - 22.1.1 Introduction to Containers
+   - 22.1.2 Introduction to Iterators
+   - 22.1.3 Introduction to Algorithms
+   
+   **22.2** Sequence Containers
+   - 22.2.1 `vector` Sequence Container
+   - 22.2.2 `list` Sequence Container
+   - 22.2.3 `deque` Sequence Container
+   
+   **22.3** Associative Containers
+   - 22.3.1 `multiset` Associative Container
+   - 22.3.2 `set` Associative Container
+   - 22.3.3 `multimap` Associative Container
+   - 22.3.4 `map` Associative Container
+   
+   **22.4** Container Adapters
+   - 22.4.1 `stack` Adapter
+   - 22.4.2 `queue` Adapter
+   - 22.4.3 `priority_queue` Adapter
+   
+   **22.5** Algorithms
+   - 22.5.1 `fill`, `fill_n`, `generate` and `generate_n`
+   - 22.5.2 `equal`, `mismatch` and `lexicographical_compare`
+   - 22.5.3 `remove`, `remove_if`, `remove_copy` and `remove_copy_if`
+   - 22.5.4 `replace`, `replace_if`, `replace_copy` and `replace_copy_if`
+   - 22.5.5 Mathematical Algorithms
+   - 22.5.6 Basic Searching and Sorting Algorithms
+   - 22.5.7 `swap`, `iter_swap` and `swap_ranges`
+   - 22.5.8 `copy_backward`, `merge`, `unique` and `reverse`
+   - 22.5.9 `inplace_merge`, `unique_copy` and `reverse_copy`
+   - 22.5.10 Set Operations
+   - 22.5.11 `lower_bound`, `upper_bound` and `equal_range`
+   - 22.5.12 Heapsort
+   - 22.5.13 `min` and `max`
+   - 22.5.14 STL Algorithms Not Covered in This Chapter
+   
+   **22.6** Class `bitset`
+   
+   **22.7** Function Objects
+   
+   **22.8** Wrap-Up
+   
+   **22.9** STL Web Resources

Summary | Terminology | Self-Review Exercises | Answers to Self-Review Exercises | Exercises | Recommended Reading

# 22.1 Introduction to the Standard Template Library (STL)

We’ve repeatedly emphasized the importance of software reuse. Recognizing that many data structures and algorithms are commonly used, the C++ standard committee added the Standard Template Library (STL) to the C++ Standard Library. The STL defines powerful, template-based, reusable components that implement many common data structures and algorithms used to process those data structures. The STL offers proof of concept for generic programming with templates—introduced in Chapter 14, Templates, and used extensively in Chapter 20, Data Structures. [Note: In industry, the features presented in this chapter are often referred to the Standard Template Library or STL. However, these terms are not used in the C++ standard documentation, because these features are simply considered to be part of the C++ Standard Library.]

The STL was developed by Alexander Stepanov and Meng Lee at Hewlett-Packard and is based on their research in the field of generic programming, with significant contributions from David Musser. As you’ll see, the STL was conceived and designed for performance and flexibility.

This chapter introduces the STL and discusses its three key components—containers (popular templated data structures), iterators and algorithms. The STL containers are data structures capable of storing objects of almost any data type (there are some restrictions).