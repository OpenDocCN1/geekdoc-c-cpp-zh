# 22.5.4.2 Constructors [unord.map.cnstr]

```
template<class Key, class T, class Hash, class Allocator>
    unordered_map(initializer_list<pair<Key, T>>, typename see below::size_type, Hash, Allocator)
        -> unordered_map<Key, T, Hash, equal_to<Key>, Allocator>;

// swap
template<class Key, class T, class Hash, class Pred, class Alloc>
    void swap(unordered_map<Key, T, Hash, Pred, Alloc>& x,
              unordered_map<Key, T, Hash, Pred, Alloc>& y)
        noexcept(noexcept(x.swap(y)));
}
```

4 A size_type parameter type in an unordered_map deduction guide refers to the size_type member type of the type deduced by the deduction guide.

```
unordered_map() : unordered_map(size_type(see below)) { }
explicit unordered_map(size_type n,
    const hasher& hf = hasher(),
    const key_equal& eql = key_equal(),
    const allocator_type& a = allocator_type());
```

1 Effects: Constructs an empty unordered_map using the specified hash function, key equality predicate, and allocator, and using at least n buckets. For the default constructor, the number of buckets is implementation-defined. max_load_factor() returns 1.0.

2 Complexity: Constant.

```
template<class InputIterator>
    unordered_map(InputIterator f, InputIterator l,
        size_type n = see below,
        const hasher& hf = hasher(),
        const key_equal& eql = key_equal(),
        const allocator_type& a = allocator_type());
unordered_map(initializer_list<value_type> il,
    size_type n = see below,
    const hasher& hf = hasher(),
    const key_equal& eql = key_equal(),
    const allocator_type& a = allocator_type());
```

3 Effects: Constructs an empty unordered_map using the specified hash function, key equality predicate, and allocator, and using at least n buckets. If n is not provided, the number of buckets is implementation-defined. Then inserts elements from the range [f, l) for the first form, or from the range [il.begin(), il.end()] for the second form. max_load_factor() returns 1.0.

4 Complexity: Average case linear, worst case quadratic.

# 22.5.4.3 Element access [unord.map.elem]

```
mapped_type& operator[](const key_type& k);
```

1 Effects: Equivalent to: return try_emplace(k).first->second;

```
mapped_type& operator[](key_type&& k);
```

2 Effects: Equivalent to: return try_emplace(move(k)).first->second;

```
mapped_type& at(const key_type& k);
const mapped_type& at(const key_type& k) const;
```

3 Returns: A reference to x.second, where x is the (unique) element whose key is equivalent to k.

4 Throws: An exception object of type out_of_range if no such element is present.

# 22.5.4.4 Modifiers [unord.map.modifiers]

```
template<class P>
    pair<iterator, bool> insert(P&& obj);
```

1 Constraints: is_constructible_v<value_type, P&&> is true.