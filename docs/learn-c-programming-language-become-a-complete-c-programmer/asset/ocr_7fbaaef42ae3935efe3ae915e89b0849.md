use only if you do a lot of vector arithmetic
A set of N bits with set operations, such as & and |
A specialization of vector<T> with compactly stored bits

For basic_string, A is the allocator (§34.4) and Tr is the character traits (§36.2.2).

Prefer a container, such as vector, string, or array, over an array when you have a choice. The implicit array-to-pointer conversion and the need to remember the size for a built-in array are major sources of errors (e.g., see §27.2.1).

Prefer the standard strings to other strings and to C-style strings. The pointer semantics of Cstyle strings imply an awkward notation and extra work for the programmer, and they are a major source of errors (such as memory leaks) (§36.3.1).

# 31.2.1 Container Representation

The standard doesn’t prescribe a particular representation for a standard container. Instead, the standard specifies the container interfaces and some complexity requirements. Implementers will choose appropriate and often cleverly optimized implementations to meet the general requirements and common uses. In addition to what is needed to manipulate elements, such a “handle” will hold an allocator (§34.4).

For a vector, the element data structure is most likely an array:
vector: rep elements free space
The vector will hold a pointer to an array of elements, the number of elements, and the capacity (the number of allocated, currently unused slots) or equivalent (§13.6).

Section 31.2.1 Container Representation 889

A list is most likely represented by a sequence of links pointing to the elements and the number of elements:
list: rep
elements: v v v

A forward_list is most likely represented by a sequence of links pointing to the elements:
forward_list: rep elements: v v v

A map is most likely implemented as a (balanced) tree of nodes pointing to (key,value) pairs:
map: rep
k k k v v v k k
v v

An unordered_map is most likely implemented as a hash table:
unordered_map: repₖ
^ hash table:
k
v kₖ vv

A string might be implemented as outlined in §19.3 and §23.2; that is, for short strings the characters are stored in the string handle itself, and for longer strings the elements are stored contiguously on the free-store (like vector elements). Like vector, a string can grow