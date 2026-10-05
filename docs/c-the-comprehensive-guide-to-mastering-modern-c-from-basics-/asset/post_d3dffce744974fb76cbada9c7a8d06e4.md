
# 26 GOOD CODE, 6TH DAN: THE RIGHT CONTAINER FOR EACH TASK

Here I provide a decision aid on which container is right for which task. In the end, I will once again concretely bring together the application of containers and algorithms, because algorithms are part of solving tasks with containers.

## 26.1 All Containers Arranged by Aspects

It is possible to find comprehensive descriptions of the behavior of any given container in a multitude of places. This allows you to select the most appropriate container for a particular scenario “simply” by reading all the documentation.

Or you can read this section, where I do it the other way around: given a scenario or important aspect, and I tell you the strengths and weaknesses of the individual containers for it. Then you can choose the container that fits the given situation.

### 26.1.1 When Is a “vector” Not the Best Choice?

First rule of thumb is this: use a vector. Only if that is not suitable should you use something else. A vector has so many good properties that there must be a good reason to decide against it:

- vector versus array: If you don't want the elements to end up on the heap, but rather managed on the stack like automatic variables, you can consider array. array does not guarantee that the memory is always managed in the same place, but in practice it is very likely the stack. Alternatively, you can also use a vector with a special allocator.
- vector versus deque: If push_back and pop_back are not enough when you also need push_front and pop_front, then use deque.
- vector versus list: If a vector grows dynamically, copying elements is expensive or impossible, and you don't know how many elements will come, then you can switch to list. It guarantees that once inserted, elements stay in place. A second reason could be that you often need to insert in the middle. In both cases, you should be aware of the management overhead of list.
- vector versus set: If all elements always need to be sorted, then use set. However, in the next section it is worth considering whether you can split your work into writing phase and a reading phase, because then vector is the best solution.
- vector versus map: If you need association from a key to target, map is usually the best choice. There are a few tips to keep in mind when using vector: You should add new elements to the back as often as possible. Do this with push_back or emplace_back. You should also remove elements from the back; the method for this is pop_back. If you already know how many elements you will insert, you should request this amount with reserve. The automatic growth of vector is surprisingly efficient, but if you can avoid it, why not?

## 26.1.2 Always Sorted: "set", "map", "multiset", and "multimap"

Before using vector (or list) to keep elements constantly sorted, you should prefer one of associative container types. Insert in the middle of vector is really expensive. Because elements are stored contiguously, in the case that insertion does not occur at the end, all elements must be shifted one position to the right. This also applies to array and deque, although the latter does not guarantee completely contiguous storage for the elements, inserting in the middle is also suboptimal. If you decide on constantly sorted vector, starting from C++23, flat_set is available. This does not nullify the cost of insertion in the middle; if you do not have many elements and they are also small, you can use flat_set. Against keeping sorted with list or even forward_list, finding insertion position takes a while because you usually have to traverse from the beginning to the desired element. This is faster in vector or array. And associative containers are specifically made for this task.

## 26.1.3 Memory Contiguous: "vector", "array"

For most applications, it is a huge advantage if the elements are densely packed in memory—and nicely in a contiguous manner. This is exactly what vector and array guarantee. There are two main reasons for this:

- Locality: When you iterate through the elements of vector, you usually start at the beginning and move toward the end in small or large jumps. The closer the memory accesses are within a unit of time, the better for the computer: memory is accessed in medium-sized blocks. For example, if you want to read only one byte, the next time you read memory near the first byte which is on the same page, it does not need to be loaded again. This is a huge time saver.
- Shared access: Writing a single large block of memory to disk is much faster than multiple small ones, and some C++ functions also take advantage of this.

## The “deque” Does Not Guarantee Contiguous Storage

Regarding the locality of elements, deque is as good as vector. The elements are very likely stored directly next to each other and therefore require very little management overhead. When you iterate through them, it is memory-friendly in one direction.

But not all elements are guaranteed to be stored next to each other. There can be several large chunks. This means there is no way to access the single memory area of the elements with data(), as is the case with array and vector. Therefore, this application is unfortunately ruled out for deque.

### 26.1.4 Cheap Insertion: "list"

Inserting a single element somewhere in the middle of a list (and forward_list) always costs a constant amount of time—called O(1) (see Chapter 24, Section 24.1.4). No other container can exhibit this property:

- vector (and deque) can insert at the end (and beginning) in O(1), but require linear time in the middle—called O(n).
- map and set (and multi variants) guarantee O(log n), and the position is determined by the sorting.
- unordered_map and unordered_set usually insert in O(1), but in the worst case, which is hard to predict, in O(n). The position of the insertion also cannot be determined and may change with further insertions.

### 26.1.5 Low Memory Overhead: "vector", "array"

If you want to store a million small elements like int, it can't be done more compactly than in vector or array. You need exactly zero bytes of additional memory per element. That's not much and can't be beaten by any other container—except perhaps deque, which requires a little additional memory for block management, but very little.

All other containers require more additional memory per element. Rarely can this be reduced with tricks:

- list stores two additional pointers per element. On a current Linux system, an int requires four bytes and a pointer requires eight bytes of memory. For one million int elements, you need four megabytes of memory with a vector. In a list, you occupy 20 megabytes.
- forward_list is specifically designed for low memory overhead. If vector (without any overhead) does not work, but the smallest possible additional footprint per element is crucial, then forward_list is preferred. However, keep in mind that you will have to deal with its specialized interface, which I advise against unless necessary.
- The ordered associative containers store their elements in a tree. Typically, this means that three additional pointers are required per element (although optimizations exist).
- The unordered associative containers maintain a hash table and a set of buckets with the actually inserted elements. The hash table holds pointers and, when well-filled, has about as much space for pointers as
