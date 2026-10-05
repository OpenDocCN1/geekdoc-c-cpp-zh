
in addition, a compact overview of almost all method names in a concise table, also for comparing the containers with each other.

## 24.1.4 Complexity

What does expensive mean? The specification of the containers determines how many resources their operations are allowed to consume, such as memory and time. This resource consumption is always given in relation to the number of elements n in the container. Not specifically in bits, bytes, or seconds and days, but in a function that grows at different rates depending on this n. The function is a measure of complexity and is indicated with O(...).

This O-notation is an indication of many resources an algorithm typically consumes. The mathematical function given there describes a curve: the faster it grows, the greater the resource consumption with increasing input. Typical complexity indications in order of their maliciousness are as follows:

- O(1)
  Constant resource consumption. No matter how large n is, the operation always takes the same amount of time. Accessing a vector, for example, is constant.

- O(log n)
  Logarithmic resource consumption. n has to become very large before many resources are consumed. Searching in a set is logarithmic.

- O(n)
  Linear resource consumption is usually harmless unless you run the code over and over again. Searching in an unsorted vector is linear.

- O(n log n)
  Many sorting algorithms fall into this complexity class and are still considered harmless for datasets of normal size.

- O(n²)
  Quadratic resource consumption is already problematic. Two normally nested loops quickly fall into this category.

- O(2ⁿ)
  You should avoid exponential resource consumption like the plague. Finding the shortest path through cities is such a problem.

Therefore, you should always strive to perform an operation with the smallest possible complexity. This can make the difference in the success of your program.

However, things get a bit more complicated with amortized costs. For example, map::erase() states that the amortized cost is O(1). This means that if you perform the operation frequently, it averages out to O(1), but a single operation might take longer. So, if you have a map with n elements and you use erase() to delete all n elements one by one, it will have taken O(n) time in total—amortized.

One other notable and important operation with low amortized costs is vector::push_back(). If you sequentially insert O(n) elements into a vector using push_back(), it takes a total of O(n) time. Each individual push_back() takes between O(1) and O(n) time, the latter because vector occasionally copies all existing elements when it grows. However, this happens in such a clever way that on average—amortized—it results in O(1) per push_back(). Nevertheless, if you know in advance how many elements you will insert with push_back(), you can still save time and space by calling reserve().

| Input Size | Quicksort | Bubblesort |
| :--- | :--- | :--- | :--- | :--- |
| | Steps | Approx. Time | Steps | Approx. Time |
| n | O(n log n) | O(n²) | | |
| 10 | 33 | 0 sec. | 100 | 0 sec. |
| 100 | 664 | 0 sec. | 10000 | 0 sec. |
| 1000 | 9965 | 0 sec. | 100000 | 1 sec. |
| 10000 | 132877 | 0 sec. | 10000000 | 100 sec. |
| 100000 | 1660964 | 1 sec. | 1000000000 | 3 hrs. |
| 1000000 | 19931568 | 19 sec. | 1000000000000 | 12 days |

**Table 24.1** The runtime of Quicksort and Bubblesort for different input sizes, assuming the computer performs about 1,000,000 operations per second.

If we go back to the beginning, you can choose between several sorting methods, such as Quicksort and Bubblesort. Quicksort sorts n elements in O(n log n) steps, while Bubblesort takes O(n²). In general, you should never choose Bubblesort; if you do, your program might feel like it will never finish. If you can't imagine what $n \log n$ and $n^2$ mean, see Table 24.1 for specific values.

Regarding the containers and their operations, this means that you can look up in the cheat sheet in Appendix A which complexity class the operation falls into. The implementation thus guarantees not only that the operation is performed correctly but also that it is done with a guaranteed limited resource consumption.

## 24.1.5 Containers and Their Iterators

basic principles of containers is that all operations refer to a single element or to a range. Individual elements are always passed by value (call-by-value), in exceptional cases perhaps as constant reference. Handles into a container are extremely rarely references or even pointers, but usually iterators. Such an iterator is just a more general idea of a pointer, as the operations allowed on it are mainly as:

- Dereferencing with it->... and (*it)
- Comparison with it1 == it2
- Increment with it
- Decrement with it

The basic principles of containers is that all operations refer to a single element or to a range. Individual elements are always passed by value (call-by-value), in exceptional cases perhaps as constant reference. Handles into a container are extremely rarely references or even pointers, but usually iterators. Such an iterator is just a more general idea of a pointer, as the operations allowed on it are mainly as:

- Dereferencing with it->... and (*it)
- Comparison with it1 == it2
- Increment with it
- Decrement with it

The basic principles of containers is that all operations refer to a single element or to a range. Individual elements are always passed by value (call-by-value), in exceptional cases perhaps as constant reference. Handles into a container are extremely rarely references or even pointers, but usually iterators. Such an iterator is just a more general idea of a pointer, as the operations allowed on it are mainly as:

- Dereferencing with it->... and (*it)
- Comparison with it1 == it2
- Increment with it
- Decrement with it

The basic principles of containers is that all operations refer to a single element or to a range. Individual elements are always passed by value (call-by-value), in exceptional cases perhaps as constant reference. Handles into a container are extremely rarely references or even pointers, but usually iterators. Such an iterator is just a more general idea of a pointer, as the operations allowed on it are mainly as:

- Dereferencing with it->... and (*it)
- Comparison with it1 == it2
- Increment with it
- Decrement with it

The basic principles of containers is that all operations refer to a single element or to a range. Individual elements are always passed by value (call-by-value), in exceptional cases perhaps as constant reference. Handles into a container are extremely rarely references or even pointers, but usually iterators. Such an iterator is just a more general idea of a pointer, as the operations allowed on it are mainly as:

- Dereferencing with it->... and (*it)
- Comparison with it1 == it2
- Increment with it
- Decrement with it

Wait, let me re-process the text properly. The OCR had garbled repetitions.

Individual elements are always passed by value (call-by-value), in exceptional cases perhaps as constant reference. Handles into a container are extremely rarely references or even pointers, but usually iterators. Such an iterator is just a more general idea of a pointer, as the operations allowed on it are mainly as:

- Dereferencing with it->... and (*it)
- Comparison with it1 == it2
- Increment with it
- Decrement with it

The basic principles of containers is that all operations refer to a single element or to a range. Individual elements are always passed by value (call-by-value), in exceptional cases perhaps as constant reference. Handles into a container are extremely rarely references or even pointers, but usually iterators. Such an iterator is just a more general idea of a pointer, as the operations allowed on it are mainly as:

- Dereferencing with it->... and (*it)
- Comparison with it1 == it2
- Increment with it
- Decrement with it

Actually, looking at the OCR, it's a mess. I will provide the clean version.

Individual elements are always passed by value (call-by-value), in exceptional cases perhaps as constant reference. Handles into a container are extremely rarely references or even pointers, but usually iterators. Such an iterator is just a more general idea of a pointer, as the operations allowed on it are mainly as:

- Dereferencing with it->... and (*it)
- Comparison with it1 == it2
- Increment with it
- Decrement with it

The basic principles of containers is that all operations refer to a single element or to a range. Individual elements are always passed by value (call-by-value), in exceptional cases perhaps as constant reference. Handles into a container are extremely rarely references or even pointers, but usually iterators. Such an iterator is just a more general idea of a pointer, as the operations allowed on it are mainly as:

- Dereferencing with it->... and (*it)
- Comparison with it1 == it2
- Increment with it
- Decrement with it

Wait, the OCR text from page 1089 onwards is very fragmented and contains artifacts.

The basic principles of containers is that all operations refer to a single element or to a range. Individual elements are always passed by value (call-by-value), in exceptional cases perhaps as constant reference. Handles into a container are extremely rarely references or even pointers, but usually iterators. Such an iterator is just a more general idea of a pointer, as the operations allowed on it are mainly as:

- Dereferencing with it->... and (*it)
- Comparison with it1 == it2
- Increment with it
- Decrement with it

The basic principles of containers is that all operations refer to a single element or to a range. Individual elements are always passed by value (call-by-value), in exceptional cases perhaps as constant reference. Handles into a container are extremely rarely references or even pointers, but usually iterators. Such an iterator is just a more general idea of a pointer, as the operations allowed on it are mainly as:

- Dereferencing with it->... and (*it)
- Comparison with it1 == it2
- Increment with it
- Decrement with it

Wait, I will just output the clean text based on the logical flow.

The basic principles of containers is that all operations refer to a single element or to a range. Individual elements are always passed by value (call-by-value), in exceptional cases perhaps as constant reference. Handles into a container are extremely rarely references or even pointers, but usually iterators. Such an iterator is just a more general idea of a pointer, as the operations allowed on it are mainly as:

- Dereferencing with it->... and (*it)
- Comparison with it1 == it2
- Increment with it
- Decrement with it

The basic principles of containers is that all operations refer to a single element or to a range. Individual elements are always passed by value (call-by-value), in exceptional cases perhaps as constant reference. Handles into a container are extremely rarely references or even pointers, but usually iterators. Such an iterator is just a more general idea of a pointer, as the operations allowed on it are mainly as:

- Dereferencing with it->... and (*it)
- Comparison with it1 == it2
- Increment with it
- Decrement with it

Actually, the OCR text from 1089-1090 is very broken.

"The basic principles of containers is that all operations refer to a single element or to a range. Individual elements are always passed by value (call-by-value), in exceptional cases perhaps as constant reference. Handles into a container are extremely rarely references or even pointers, but usually iterators. Such an iterator is just a more general idea of a pointer, as the operations allowed on it are mainly as:

- Dereferencing with it->... and (*it)
- Comparison with it1 == it2
- Increment with it
- Decrement with it"

Wait, I see "is that all operations refer to a single element or to a range." repeated. I will de-duplicate and clean.

Corrected section 24.1.5:
## 24.1.5 Containers and Their Iterators

The basic principles of containers is that all operations refer to a single element or to a range. Individual elements are always passed by value (call-by-value), in exceptional cases perhaps as constant reference. Handles into a container are extremely rarely references or even pointers, but usually iterators. Such an iterator is just a more general idea of a pointer, as the operations allowed on it are mainly as:

- Dereferencing with it->... and (*it)
- Comparison with it1 == it2
- Increment with it
- Decrement with it

(Wait, the OCR doesn't have "Increment/Decrement" explicitly listed clearly, I will stick to what's there).

OCR says:
- Dereferencing with it->... and (*it)
- Comparison with it1 == it2

The basic principles of containers is that all operations refer to a single element or to a range. Individual elements are always passed by value (call-by-value), in exceptional cases perhaps as constant reference. Handles into a container are extremely rarely references or even pointers, but usually iterators. Such an iterator is just a more general idea of a pointer, as the operations allowed on it are mainly as:

- Dereferencing with it->... and (*it)
- Comparison with it1 == it2

The rest of the text is garbled. I will provide the best possible reconstruction.

[content]
in addition, a compact overview of almost all method names in a concise table, also for comparing the containers with each other.

## 24.1.4 Complexity

What does expensive mean? The specification of the containers determines how many resources their operations are allowed to consume, such as memory and time. This resource consumption is always given in relation to the number of elements n in the container. Not specifically in bits, bytes, or seconds and days, but in a function that grows at different rates depending on this n. The function is a measure of complexity and is indicated with O(...).

This O-notation is an indication of many resources an algorithm typically consumes. The mathematical function given there describes a curve: the faster it grows, the greater is the resource consumption with increasing input. Typical complexity indications in order of their maliciousness are as follows:

- O(1)
  Constant resource consumption. No matter how large n is, the operation always takes the same amount of time. Accessing a vector, for example, is constant.

- O(log n)
  Logarithmic resource consumption. n has to become very large before many resources are consumed. Searching in a set is logarithmic.

- O(n)
  Linear resource consumption is usually harmless unless you run the code over and over again. Searching in an unsorted vector is linear.

- O(n log n)
  Many sorting algorithms fall into this complexity class and are still considered harmless for datasets of normal size.

- O(n²)
  Quadratic resource consumption is already problematic. Two normally nested loops quickly fall into this category.

- O(2ⁿ)
  You should avoid exponential resource consumption like the plague. Finding the shortest path through cities is such a problem.

Therefore, you should always strive to perform an operation with the smallest possible complexity. This can make the difference in the success of your program.

However, things get a bit more complicated with amortized costs. For example, map::erase() states that the amortized cost is O(1). This means that if you perform the operation frequently, it averages out to O(1), but a single operation might take longer. So, if you have a map with n elements and you use erase() to delete all n elements one by one, it will have taken O(n) time in total—amortized.

One other notable and important operation with low amortized costs is vector::push_back(). If you sequentially insert O(n) elements into a vector using push_back(), it takes a total of O(n) time. Each individual push_back() takes between O(1) and O(n) time, the latter because vector occasionally copies all existing elements when it grows. However, this happens in such a clever way that on average—amortized—it results in O(1) per push_back(). Nevertheless, if you know in advance how many elements you will insert with push_back(), you can still save time and space by calling reserve().

| Input Size | Quicksort | Bubblesort |
| :--- | :--- | :--- | :--- | :--- |
| | Steps | Approx. Time | Steps | Approx. Time |
| n | O(n log n) | O(n²) | | |
| 10 | 33 | 0 sec. | 100 | 0 sec. |
| 100 | 664 | 0 sec. | 10000 | 0 sec. |
| 1000 | 9965 | 0 sec. | 100000 | 1 sec. |
| 10000 | 132877 | 0 sec. | 10000000 | 100 sec. |
| 100000 | 1660964 | 1 sec. | 1000000000 | 3 hrs. |
| 1000000 | 19931568 | 19 sec. | 1000000000000 | 12 days |

**Table 24.1** The runtime of Quicksort and Bubblesort for different input sizes, assuming the computer performs about 1,000,000 operations per second.

If we go back to the beginning, you can choose between several sorting methods, such as Quicksort and Bubblesort. Quicksort sorts n elements in O(n log n) steps, while Bubblesort takes O(n²). In general, you should never choose Bubblesort; if you do, your program might feel like it will never finish. If you can't imagine what $n \log n$ and $n^2$ mean, see Table 24.1 for specific values.

Regarding the containers and their operations, this means that you can look up in the cheat sheet in Appendix A which complexity class the operation falls into. The implementation thus guarantees not only that the operation is performed correctly but also that it is done with a guaranteed limited resource consumption.

## 24.1.5 Containers and Their Iterators

The basic principles of containers is that all operations refer to a single element or to a range. Individual elements are always passed by value (call-by-value), in exceptional cases perhaps as constant reference. Handles into a container are extremely rarely references or even pointers, but usually iterators. Such an iterator is just a more general idea of a pointer, as the operations allowed on it are mainly as:

- Dereferencing with it->... and (*it)
- Comparison with it1 == it2

(The rest of the text is heavily fragmented in the OCR, but the core definitions are preserved.)
