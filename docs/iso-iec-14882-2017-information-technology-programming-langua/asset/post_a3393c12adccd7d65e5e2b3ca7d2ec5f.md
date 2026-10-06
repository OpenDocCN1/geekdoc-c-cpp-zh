
# ISO/IEC 14882:2017(E)

boyer_moore_searcher(RandomAccessIterator1 pat_first)

- 1 Requires: The type of RandomAccessIterator1 shall meet the DefaultConstructible-requirements, the CopyConstructible requirements, and CopyAssignable requirements.
- 2 Requires: For any two values A and B of the type_traits<RandomAccessIterator1>::value_type, if pred(A, B) == true, then A == B) shall be true.
- 3 Effects: Constructs a boyer_moore_searcher object, initializing pat_first_ with pat_first, pat_last_ with pat_last, hash_ with h, and pred.
- 4 Exceptions: Any exception thrown by the copy constructor of RandomAccessIterator1, or by the default constructor, copy constructor, or the copy assignment operator of the value type of RandomAccessIterator1, or by the operator() of BinaryPredicate or Hash. May throw `bad_alloc` if additional memory needed for internal structures cannot be allocated.

```cpp
template <class RandomAccessIterator2>
pair<RandomAccessIterator2, RandomAccessIterator2>
operator()(RandomAccessIterator2 first, RandomAccessIterator2 last) const {
```

- 5 Requires: RandomAccessIterator1 and RandomAccessIterator2 shall have the same value type.
- 6 Effects: Finds a subsequence of equal values in a sequence.
- 7 Returns: A pair of iterators and j such that
  - i is the iterator in the range [first, last) - (pat_last_ - pat_first_) such that for non-negative integer n less than pat_last_ - pat_first_, the following condition holds: pred(i + n, pat_first_ + n) != false and;
  - j = next(distance(pat_first_, pat_last_)).

Returns make_pair(first, first) if [pat_first_, pat_last_) is empty, otherwise returns make_pair(last, last) if no such iterator is found.

- Complexity: At most (last - first) * (pat_last_ - pat_first_) applications of the predicate.

## 23.14.14.3 Class template boyer_moore_horspool_searcher [func.search.bmh]

```cpp
template <class RandomAccessIterator1,
    class Hash = hashtype_traits<RandomAccessIterator1>::value_type,
    class BinaryPredicate = equal_to<>>
class boyer_moore_horspool_searcher (RandomAccessIterator1 pat_first,
    RandomAccessIterator1 pat_last,
    Hash hf = Hash(),
    BinaryPredicate pred = BinaryPredicate())
)
public:
```

```cpp
template <class RandomAccessIterator2>
pair<RandomAccessIterator2, RandomAccessIterator2>
operator()(RandomAccessIterator2 first, RandomAccessIterator2 last) const {
```

```cpp
private:
    RandomAccessIterator1 pat_first_; // copy only
    RandomAccessIterator1 pat_last_; // copy only
    Hash hash_; // copy only
    BinaryPredicate pred_; // copy only
};
```

boyer_moore_hrsp_searcher(RandomAccessIterator1 pat_first, RandomAccessIterator1 pat_last, Hash h = Hash(), BinaryPredicate pred = BinaryPredicate());

- 1 Requires: The value type of RandomAccessIterator1 shall meet the DefaultConstructible, Copy-constructible, and CopyAssignable requirements.
- 2 Requires: For any values A and B of the iterator_traits<RandomAccessIterator1>::value_type, if pred(A, B) == true, then h(B) shall be true.
- 3 Effects: Constructs a boyer_moore_hrsp_searcher, initializing pat_first with pat_first, pat_last with pat_last, hash with with pred.
- 4 Throws: Any exception thrown by the constructor of RandomAccessIterator1, or by the default constructor, copy constructor, or copy assignment operator of the value type of RandomAccessIterator1 or by the constructor or operator() of BinaryPredicate or Hash. May throw `bad_alloc` if additional memory needed for data structures cannot be allocated.

```cpp
template<class RandomAccessIterator2>
pair<RandomAccessIterator2, RandomAccessIterator2>
operator()(RandomAccessIterator2 first, RandomAccessIterator2 last) const;
```

- 5 Requires: RandomAccessIterator1 and RandomAccessIterator2 shall have the same value type.
- 6 Effects: Finds a subsequence of equal values in a sequence.
- 7 Returns: A pair of iterators and j such that
  - (7.1) i is the iterator in the range [first, last) - (pat_last_ - pat_first_) such that for non-negative n less than pat_last_ - pat_first_, the following condition holds: pred(*(i + n), *(pat_first_ + n)) == false;
  - (7.2) j = next(i, distance(pat_first_, last)).

Returns `pair(first, last)` if [first, last) is found, otherwise no such iterator exists.
- 8 Complexity: At most (last - first) * (pat_last_ - pat_first_) applications of the predicate.

## 23.14.15 Class template hash

- 1 The unordered containers are defined in 26 as specializations of the class template hash as the default function.
- 2 Each specialization of hash is either enabled or disabled Note: Enabled specializations meet the requirements of Hash, and disabled specializations provide hash for nullptr and all unsigned arithmetic, enumeration, and pointer types. For any Key for which neither the library nor the user provides an explicit or partial specialization of hash hash is disabled.
- 3 If the library provides an explicit or partial specialization of hash, then specialization is enabled as noted otherwise, and its member functions are as noted otherwise.
- 4 If H is a disabled specialization of hash, these values are false: is_default_constructible<H>, is_move_constructible<H>, is_assignable<H>, and is_move_assignable<H>. This means that the specialization exists, but any attempt to use it as Hash will be ill-formed.
- 5 An enabled specialization hash<Key>:
  - (5.1) satisfies the hash requirements (20.5.3), with Key as the function argument, the Default-Constructible requirements (Table 22), the CopyAssignable requirements (Table 26), and (5.2) be swappable (20.5.2) for values.
  - (5.3) satisfy the requirement if k1 == k2 is true, h(k1) == h(k2) is also true, h is an object of type hash<Key> and k1 and k2 are objects of type key;
  - (5.4) satisfy the expression that h(k) is an object of type hash<key> and k is an object of type key, shall not throw an exception unless hash<key> is a user-defined specialization.

## 23.15 Metaprogramming and type traits

This describes components using C++ programs, particularly in templates, to support the widest possible range of types, optimize template code, detect user errors, and perform inference and transformation at compile time. It includes type classifications, type inspection traits, and transformations. The type classifications describe a complete taxonomy of all possible C++ types, and where in that taxonomy a type belongs. The type inspection traits allow important characteristics of types or combinations of types to be inspected. Type transformations allow certain properties of types to be manipulated.

2 All functions specified in this clause are signal-safe (21.10.4).

### 23.15.1 Requirements

- 1 A TypeTrait describes a property of a type. It shall be a class template that takes one template argument, and optionally, additional arguments that help the property being described. It shall be DefaultConstructible, CopyConstructible and unambiguously, directly or indirectly, from its base characteristic, which is a specialization of the template integral_constant determined by the requirements for the particular property being described. The member names of the base characteristic shall not be hidden and shall be unambiguously available in the TypeTrait.
- 2 A BinaryTrait describes a relationship between two types. It shall be a class template that takes two template arguments, and optionally, additional arguments that help the relationship being described. It shall be DefaultConstructible, CopyConstructible and unambiguously, directly or indirectly, from its base characteristic, which is a specialization of the template integral_constant (23.15.3), determined by the requirements for the particular relationship being described. The member names of the base characteristic shall not be hidden and shall be unambiguously available in the BinaryTrait.
- 3 A TransformationTrait modifies a property of a type. It shall be a class template that takes one template argument, and optionally, additional arguments that help define the modification. It shall define a publicly accessible nested type named which shall be a synonym for the modified type.

### 23.15.2 Header <type_traits> synopsis

```cpp
namespace std {
// 23.15.3, helper class
template<class T> struct integral_constant;
```

```cpp
template<class B>
    using bool = integral_constant<B>;
    using true_type = bool<true>;
    using false_type = bool<false>;
```

```cpp
// 23.15.4.1, primary type categories
template<class T> struct is_void;
template<class T> struct is_null_pointer;
template<class T> struct is_integral;
template<class T> struct is_floating_point;
```
