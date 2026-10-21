other objects. We will be looking at a few of the components of this library in due course:

+   1. Vector (implementation is like an array), list (implementation of doubly linked list), and deque (implementation of deque) are called *sequence containers*.
+   2. Set, multiset, map, and multimap are known as *associative sorted containers*. Unlike sequence containers, these containers keep the contents in a sorted form.
+   3. There are adapted containers such as queue and stack that are not true containers but are implemented using sequence containers.

# Iterators

One can think of iterators as generic pointers. The designers of C used void pointers in many cases where they would like a pointer to be assigned to any other type later. malloc() is an excellent example; it returns the void pointer that a programmer can assign to the type he/she deems fit. In true sense, iterators are far more capable than void pointers.

If there is an array, one will traverse the array using an index. On the contrary, if there is a linked list, one can traverse it using a pointer designed to point to the node of that linked list. If some other structure is used, then some other mechanism is needed to traverse the container. The array index used to traverse an array sequentially or randomly and the pointer used in a linked list to traverse the list sequentially are basically doing the same job, which is, traversing a sequence of elements. In the case of STL, a generalized concept called iterator is used to traverse a sequence of container elements.

An important problem in generalizing such a concept is to ensure that it is not bound to a type. For example, consider designing a pointer that can be used to point to any linked list node; it is just impossible. Say, if there is a linked list of integers, the pointer to be used is int*, and if there is a linked list of node of type NodeType, the pointer to be used is NodeType*. In such a situation, templates are used to avoid type-related issues. For example, if there is a pointer defined as Type *ptr, the ptr is a generic pointer. Iterator is a kind of generic index that helps one to iterate through some specific sequence. The following code segment helps us understand the same.

```
vector <int>::iterator IntIndex;

for(IntIndex = vi.begin(); IntIndex < vi.end(); IntIndex++)
{
    cout << *IntIndex << endl;
}
```

The IntIndex variable is of type iterator (of vector int type), which will help one iterate through a vector (a container type quite similar to an array) vi. We will soon see other details about how to program with containers, generic algorithms, and containers.

Iterators, thus, help a user to iterate through a sequence of elements of a container; hence, the name.

The beauty of matching generic algorithms with generic containers lies in the use of templates and objects known as iterators. They are pointer-like objects, but unlike pointers, they are categorized into five different categories, namely, input, random access, bidirectional, forward, and output.

Generic algorithms are written to work on iterator objects rather than any data structure. The find() algorithm works on a category of iterators called *input iterators*.