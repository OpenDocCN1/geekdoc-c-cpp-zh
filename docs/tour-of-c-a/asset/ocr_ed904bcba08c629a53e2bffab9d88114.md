| multiset<T> | A set in which value can occur many times |
| unordered_set<T> | A set using a hashed lookup |
| unordered_multiset<T> | A multiset using a hashed lookup |

The unordered containers are optimized for lookup with a value (often a string); in other words, they are hashes.
The containers are defined in namespace std and presented in headers <vector>, <list>, <map>, etc. ($9.3.4). In addition, the standard library provides container adapters queue<T>, stack<T>, and priority_queue<T>. Look them up if you need them. The standard library also provides specialized container-like types, such as array<T,N> ($15.3.1) and bitset<N> ($15.3.2).
The standard containers and their basic operations are designed to be simple from a notational point of view. Furthermore, the meanings of operations are equivalent for the various kind of container. Basic operations apply to which they make sense and can be implemented:

| value_type | The type of element |
| p=c.begin() | p points to first element of c; also cbegin() for an iterator const
| p=c.end() | p points to one-past-the-element of c;
end() for an iterator const
k=c.size() | k is the number of elements in c
| c.empty() | Is c empty?
k=c.capacity() | k is the number of elements that c can hold without a new allocation
| c.reserve(k) | Increase the capacity to k; if k<c.capacity(), c.reserve(k) does nothing
| c.resize(k) | Make the number of elements k; added elements have the default value_type() |
| c[k] | The kth element of c; zero-based; no out of range, throw out_of_range
| c.push_back(x) | Add x to the end of c; increase the size of c by one
| c.emplace_back(a) | Add value_type(a) at the end of c; increase the size of c by one
| q.insert(p,x) | Add x before p in c
| q.erase(p) | Remove element p from c
| c=c2 | Assignment: copy all elements from c2 to get c==c2
| b=(c==c2) | Equality of elements of c and c2; b==true if equal
xs=(c<c2) | Lexicographical order of c and c2:
x<0 if c is less than c2, x=0 if equal, and 0<x if greater.
!=, <=, <, and >= are generated from <= |

This notational and semantic uniformity enables programmers to provide new container types