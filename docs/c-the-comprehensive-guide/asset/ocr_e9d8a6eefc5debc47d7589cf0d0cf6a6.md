+   - `unordered_map` and `unordered_set` usually insert in O(1), but in the worst case, which is hard to predict, in O(n). The position of the insertion also cannot be determined and may change with further insertions.

# 26.1.5  Low Memory Overhead: “vector”, “array”

If you want to store a million small elements like it, it can't be done more compactly than in `vector` or `array`. You need exactly zero bytes of additional memory per element. That's not much and can't be beaten by any other container—except perhaps `deque`, which requires a little additional memory for block management, but very little.

All other containers require more additional memory per element. Rarely can this be reduced with tricks:

+   - `list` stores two additional pointers per element. On a current Linux system, an `int` requires four bytes and a pointer requires eight bytes of memory. For one million `int` elements, you need four megabytes of memory with a `vector`. In a `list`, you would occupy 20 megabytes.
+   - `forward_list` is specifically designed for low memory overhead. If `vector` (without any overhead) does not work, but the smallest possible additional footprint per element is crucial, then `forward_list` is preferred. However, keep in mind that you will have to deal with its specialized interface, which I advise against unless necessary.
+   - The ordered associative containers store their elements in a tree. Typically, this means that three additional pointers are required per element (although optimizations exist).
+   - The unordered associative containers maintain a hash table and a set of buckets with the actually inserted elements. The hash table holds pointers and, when well-filled, has about as much space for pointers as you have elements in the container. The buckets are usually implemented as `forward_list`. All in all, you need an estimated two additional pointers of space per element in your container.

Besides the additional memory required per element, there is another factor you need to consider: It is much worse to request 1,000 bytes 1,000 times than to request 1,000,000 bytes once. This is because the system also requires some memory for each requested memory block. It gets even worse if you also release blocks in between. Then it depends on how well your system can reuse memory—and that is an arbitrarily difficult problem.

What can happen is that the memory *fragments*. The bad thing is that it happens without you noticing, hidden from you. Your program has no way to detect fragmentation.