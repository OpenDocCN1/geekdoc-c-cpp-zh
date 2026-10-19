

## ISO/IEC 14882:2020(E)

Table 79: Container types with compatible nodes [tab:container.node.compat]

| map<K, T, C1, A> | map<K, T, C2, A> |
| map<K, T, C1, A> | multimap<K, T, C2, A> |
| set<K, C1, A> | set<K, C2, A> |
| set<K, C1, A> | multiset<K, C2, A> |
| unordered_map<K, T, H1, E1, A> | unordered_map<K, T, H2, E2, A> |
| unordered_map<K, T, H1, E1, A> | unordered_multimap<K, T, H2, E2, A> |
| unordered_set<K, H1, E1, A> | unordered_set<K, H2, E2, A> |
| unordered_set<K, H1, E1, A> | unordered_multiset<K, H2, E2, A> |

3 Class node-handle is for exposition only.

4 If a user-defined specialization of pair exists for pair<const Key, T> or pair<Key, T>, where Key is the container's key_type and T is the container's mapped_type, the behavior of operations involving node handles is undefined.

```
template<unspecified>
class node-handle {
public:
    // These type declarations are described in Tables 80 and 81.
    using value_type      = see below;      // not present for map containers
    using key_type        = see below;      // not present for set containers
    using mapped_type     = see below;      // not present for set containers
    using allocator_type  = see below;

private:
    using container_node_type = unspecified;
    using ator_traits = allocator_traits<allocator_type>;

    typename ator_traits::template rebind_traits<container_node_type>::pointer ptr_;
    optional<allocator_type> alloc_;

public:
    // 22.2.4.2, constructors, copy, and assignment
    constexpr node-handle() noexcept : ptr_(), alloc_() {}
    node-handle(node-handle&&) noexcept;
    node-handle& operator=(node-handle&&);

    // 22.2.4.3, destructor
    ~node-handle();

    // 22.2.4.4, observers
    value_type& value() const;              // not present for map containers
    key_type& key() const;                  // not present for set containers
    mapped_type& mapped() const;            // not present for set containers

    allocator_type get_allocator() const;
    explicit operator bool() const noexcept;
    [[nodiscard]] bool empty() const noexcept;

    // 22.2.4.5, modifiers
    void swap(node-handle&)
        noexcept(ator_traits::propagate_on_container_swap::value ||
                 ator_traits::is_always_equal::value);

    friend void swap(node-handle& x, node-handle& y) noexcept(noexcept(x.swap(y))) {
        x.swap(y);
    }
};
```

## 22.2.4.2 Constructors, copy, and assignment [container.node.cons]

```
node-handle(node-handle&& nh) noexcept;
```

Effects: Constructs a node-handle object initializing ptr_ with nh.ptr_. Move constructs alloc_ with nh.alloc_. Assigns nullptr to nh.ptr_ and assigns nullopt to nh.alloc_.

```
node-handle& operator=(node-handle&& nh);
```

Preconditions: Either !alloc_, or allocator_traits::propagate_on_container_move_assignment::value is true, or alloc_ == nh.alloc_.

Effects:

- If ptr_ != nullptr, destroys the value_type subobject in the container_node_type object pointed to by ptr_ by calling allocator_traits::destroy, then deallocates ptr_ by calling allocator_traits::template rebind_traits<container_node_type>::deallocate.
- Assigns nh.ptr_ to ptr_.
- If !alloc_ or allocator_traits::propagate_on_container_move_assignment::value is true, move assigns nh.alloc_ to alloc_.
- Assigns nullptr to nh.ptr_ and assigns nullopt to nh.alloc_.

Returns: *this.

Throws: Nothing.

## 22.2.4.3 Destructor [container.node.dtor]

```
~node-handle();
```

Effects: If ptr_ != nullptr, destroys the value_type subobject in the container_node_type object pointed to by ptr_ by calling allocator_traits::destroy, then deallocates ptr_ by calling allocator_traits::template rebind_traits<container_node_type>::deallocate.

## 22.2.4.4 Observers [container.node.observers]

```
value_type& value() const;
```

Preconditions: empty() == false.

Returns: A reference to the value_type subobject in the container_node_type object pointed to by ptr_.

Throws: Nothing.

```
key_type& key() const;
```

Preconditions: empty() == false.

Returns: A non-const reference to the key_type member of the value_type subobject in the container_node_type object pointed to by ptr_.

Throws: Nothing.

Remarks: Modifying the key through the returned reference is permitted.

```
mapped_type& mapped() const;
```

Preconditions: empty() == false.

Returns: A reference to the mapped_type member of the value_type subobject in the container_node_type object pointed to by ptr_.

Throws: Nothing.

```
allocator_type get_allocator() const;
```

## ISO/IEC 14882:2020(E)

Table 80: Associative container requirements (in addition to container) (continued)

| Expression | Return type | Assertion/note pre-/post-condition | Complexity |
|---|---|---|---|
| X(c)
X u(c); |  | Effects: Constructs an empty container. Uses a copy of c as a comparison object. | constant |
| X()
X u; |  | Preconditions: key_compare meets the Cpp17DefaultConstructible requirements.
Effects: Constructs an empty container. Uses Compare() as a comparison object | constant |
| X(i,j,c)
X u(i,j,c); |  | Preconditions: value_type is Cpp17EmplaceConstructible into X from *i.
Effects: Constructs an empty container and inserts elements from the range [i, j) into it; uses c as a comparison object. | N log N in general, where N has the value distance(i, j); linear if [i, j) is sorted with value_comp() |
| X(i,j)
X u(i,j); |  | Preconditions: key_compare meets the Cpp17DefaultConstructible requirements. value_type is Cpp17EmplaceConstructible into X from *i.
Effects: Same as above, but uses Compare() as a comparison object. | same as above |
| X(il) |  | same as X(il.begin(), il.end()) | same as X(il.begin(), il.end()) |
| X(il,c) |  | same as X(il.begin(), il.end(), c) | same as X(il.begin(), il.end(), c) |
| a = il | X& | Preconditions: value_type is Cpp17CopyInsertable into X and Cpp17CopyAssignable.
Effects: Assigns the range [il.begin(), il.end()) into a. All existing elements of a are either assigned to or destroyed. | N log N in general, where N has the value il.size() + a.size(); linear if [il.begin(), il.end()) is sorted with value_comp() |
| b.key_-comp() | X::key_-compare | Returns: the comparison object out of which b was constructed. | constant |
| b.value_-comp() | X::value_-compare | Returns: an object of value_compare constructed out of the comparison object | constant |

## ISO/IEC 14882:2020(E)

Table 80: Associative container requirements (in addition to container) (continued)

| Expression | Return type | Assertion/note pre-/post-condition | Complexity |
|---|---|---|---|
| a_uniq. emplace(args) | pair<iterator, bool> | Preconditions: value_type is Cpp17EmplaceConstructible into X from args.
Effects: Inserts a value_type object t constructed with std::forward<Args>(args)... if and only if there is no element in the container with key equivalent to the key of t. The bool component of the returned pair is true if and only if the insertion takes place, and the iterator component of the pair points to the element with key equivalent to the key of t. | logarithmic |
| a_eq. emplace(args) | iterator | Preconditions: value_type is Cpp17EmplaceConstructible into X from args.
Effects: Inserts a value_type object t constructed with std::forward<Args>(args)... and returns the iterator pointing to the newly inserted element. If a range containing elements equivalent to t exists in a_eq, t is inserted at the end of that range. | logarithmic |
| a.emplace_hint(p, args) | iterator | equivalent to a.emplace(std::forward<Args>(args)...). Return value is an iterator pointing to the element with the key equivalent to the newly inserted element. The element is inserted as close as possible to the position just prior to p. | logarithmic in general, but amortized constant if the element is inserted right before p |
| a_uniq. insert(t) | pair<iterator, bool> | Preconditions: If t is a non-const rvalue, value_type is Cpp17MoveInsertable into X; otherwise, value_type is Cpp17CopyInsertable into X.
Effects: Inserts t if and only if there is no element in the container with key equivalent to the key of t. The bool component of the returned pair is true if and only if the insertion takes place, and the iterator component of the pair points to the element with key equivalent to the key of t. | logarithmic |

