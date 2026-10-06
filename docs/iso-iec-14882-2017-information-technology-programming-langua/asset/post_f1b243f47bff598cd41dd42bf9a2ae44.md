
ISO/IEC 14882:2017(E)

- 11 Returns: The first argument when the arguments are equivalent.
- 12 Complexity: Exactly one comparison.

```cpp
template<class T>
constexpr T max(initializer_list<T> t);
template<class T, class Compare> max(initializer_list<T> t, Compare comp);
```

- 13 Requires: T shall be CopyConstructable and t.size() > 0. For the first form, type T shall be LessThanComparable.
- 14 Returns: The largest value in the initializer_list.
- 15 Returns: A copy of the leftmost argument when several arguments are equivalent to the largest.
- 16 Complexity: Exactly t.size() - 1.

```cpp
template<class T> constexpr min(const T& a, const T& b);
template<class T, class Compare> min(const T& a, const T& b);
constexpr pair<const T&, const T&> min(const T& a, b);
```

- 17 Requires: For the first form, type T shall be LessThanComparable (Table 21).
- 18 Returns: pair<const T&, const T&> if b is smaller than a, and pair<const T&, const T&>(a, b) otherwise.
- 19 Remarks: pair<const T&, const T&>(a, b) when the arguments are equivalent.
- 20 Complexity: Exactly one comparison.

```cpp
template<class T> min(initializer_list<T> t);
template<class T, class Compare> min(initializer_list<T> t, Compare comp);
```

- 21 Requires: T shall be CopyConstructible and t.size() > 0. For the first form, type T shall be LessThanComparable.
- 22 Returns: pair<T, T>(x, y), where x has the smallest and y has the largest value in the initializer list. y is a copy of the rightmost argument when several arguments are equivalent to the smallest.
- 23 Complexity: At (3/2).size() applications of the corresponding predicate.

```cpp
template<class Forwarditerator>
constexpr Forwarditerator min_element(Forwarditerator first, Forwarditerator last);
```

```cpp
template<class Forwarditerator, class ExecutionPolicy>
Forwarditerator min_element(ExecutionPolicy&& exec, Forwarditerator first, Forwarditerator last);
```

```cpp
template<class Forwarditerator, class Compare>
constexpr Forwarditerator min_element(Forwarditerator first, Forwarditerator last, Compare comp);
```

```cpp
template<class Forwarditerator, class ExecutionPolicy, class Compare>
Forwarditerator min_element(ExecutionPolicy&& exec, Forwarditerator first, Forwarditerator last, Compare comp);
```

- 25 Returns: The first iterator i in the range [first, last) such that for every iterator j in the range [first, last), the following condition holds: !(*j < *i) or comp(*j, *i) == false.

Returns last if first == last.
Complexity: Exactly max(last - first, 1.0) applications of the corresponding comparisons.

```cpp
template<class ForwardIterator>
const& ForwardIterator max_element(ForwardIterator first, ForwardIterator last);
template<class ExecutionPolicy, class ForwardIterator>
ForwardIterator max_element(ExecutionPolicy&& exec, ForwardIterator first, ForwardIterator last);

template<class Compare>
const& ForwardIterator max_element(ForwardIterator first, ForwardIterator last, Compare comp);
template<class ExecutionPolicy, class ForwardIterator, class Compare>
ForwardIterator max_element(ExecutionPolicy&& exec, ForwardIterator first, ForwardIterator last, Compare comp);
```

Returns: The first iterator in the range [first, last) that for every j in the range [first, last) the following condition holds: !(*i < j) or comp(*i,j) == false.
Returns last if first == last.
Complexity: Exactly max(last - first, 1.0) applications of the corresponding comparisons.

```cpp
template<class ForwardIterator>
const pair<ForwardIterator, ForwardIterator>
max_element(ForwardIterator first, ForwardIterator last);
template<class ExecutionPolicy, class ForwardIterator>
pair<ForwardIterator, ForwardIterator>
max_element(ExecutionPolicy&& exec, ForwardIterator first, ForwardIterator last);

template<class ForwardIterator, class Compare>
const pair<ForwardIterator, ForwardIterator>
max_element(ForwardIterator first, ForwardIterator last, Compare comp);
template<class ExecutionPolicy, class ForwardIterator, class Compare>
pair<ForwardIterator, ForwardIterator>
max_element(ExecutionPolicy&& exec, ForwardIterator first, ForwardIterator last, Compare comp);
```

Returns: max_pair(first, first) if [first, last) is empty, otherwise make_pair(m, M), where m is the first iterator in [first, last) such that no iterator in the range refers to a smaller element, and M is the last iterator in [first, last) such that no iterator in the range refers to a larger element.
Complexity: At most max(|N-1|, 1.0) applications of the corresponding predicate, where N is last - first.

## 28.9. Bounded value [alg.clamp]

```cpp
template<class T>
const T& clamp(const T& v, const T& lo, const T& hi);
template<class Compare>
const T& clamp(const T& v, const T& lo, const T& hi, Compare comp);
```

- Requires: The value of lo should not be greater than hi. For the first form, type T is LessThanComparable (Table 21).
- This behavior intentionally differs from max_element().
- Returns: lo if v is less than hi, hi is less than v, otherwise v.
- Note: NaN is avoided, T can be a floating-point type.
Complexity: At most two comparisons.

## 28.7.10 Lexographical comparison [alg.comparison]

```cpp
template<class InputIterator, class InputIterator>
bool
lexicographical_compare(InputIterator first1, InputIterator last1, InputIterator first2, InputIterator last2);
template<class ExecutionPolicy, class ForwardIterator, class ForwardIterator>
bool
lexicographical_compare(ExecutionPolicy&& exec, ForwardIterator first1, ForwardIterator last1, ForwardIterator first2, ForwardIterator last2);
template<class InputIterator, class InputIterator, class Compare>
bool
lexicographical_compare(InputIterator first1, InputIterator last1, InputIterator first2, InputIterator last2, Compare comp);
template<class ExecutionPolicy, class ForwardIterator, class ForwardIterator, class Compare>
bool
lexicographical_compare(ExecutionPolicy&& exec, ForwardIterator first1, ForwardIterator last1, ForwardIterator first2, ForwardIterator last2, Compare comp);
```

Returns: true if the sequence of elements defined by the range [first1, last1) is lexicographically less than the sequence of elements defined by the range [first2, last2) and false otherwise.
Complexity: If two sequences have the same number of elements and their corresponding elements (if any) are equivalent, then neither is lexicographically less than the other. If one sequence is a prefix of the other, then the shorter sequence is lexicographically less than the longer sequence. Otherwise, the lexicographical comparison yields the same result as the comparison of the first corresponding pairs of elements that are not equal.
Example: The following implementation satisfies these requirements:
```cpp
for (; first1 != last1 && first2 != last2; ++first1, ++first2) {
    if (*first1 < *first2) return false;
    if (*first2 < *first1) return true;
}
return first1 == last1 && first2 == last2;
```
Note: An empty sequence is lexicographically less than any non-empty sequence, but not less than any sequence.

## 28.7.11 Permutation generators [alg.permutation.generators]

```cpp
template<class BidirectionalIterator>
bool next_permutation(BidirectionalIterator first, BidirectionalIterator last);
```

## ISO/IEC 14882:2017(E)

```cpp
template<class BidirectionalIterator, class Compare>
bool next_permutation(BidirectionalIterator first, BidirectionalIterator last, Compare comp);
```

- 1 Requires: BidirectionalIterator shall satisfy the requirements of ValueSwapable (20.5.3.2).
- 2 Effects: Takes a sequence defined by the range [first, last] and transforms it into the next permutation. The next permutation is found by assuming that the set of all permutations is lexicographically sorted with respect to operator< or comp.
- 3 Returns: true if such a permutation exists. Otherwise, it transforms the sequence into the largest permutation, that is descendingly sorted, and returns false.
- 4 Complexity: At most (last - first) / 2 swaps.

```cpp
template<class BidirectionalIterator>
bool prev_permutation(BidirectionalIterator first, BidirectionalIterator last);
template<class BidirectionalIterator, class Compare>
bool prev_permutation(BidirectionalIterator first, BidirectionalIterator last, Compare comp);
```

- 5 Requires: BidirectionalIterator shall satisfy the requirements of ValueSwapable (20.5.3.2).
- 6 Effects: Takes a sequence defined by the range [first, last] and transforms it into the previous permutation. The previous permutation is found by assuming that the set of all permutations is lexicographically sorted with respect to operator< or comp.
- 7 Returns: true if such a permutation exists. Otherwise, it transforms the sequence into the smallest permutation, that is descendingly sorted, and returns false.
- 8 Complexity: At most (last - first) / 2 swaps.

## 28.8 C algorithms

Note: The header <cstdlib> (21.2.2) declares the functions described in this subclause. — end note

```c
void* search(const void* key, const void* base, size_t nemb, size_t size,
               int (*compare_pred)(const void*, const void*));
void qsort(void* base, size_t nemb, size_t size, int (*compare_pred)(const void*, const void*));
```

- 2 Effects: These functions have the semantics specified in the C standard library.
- 3 Remarks: The behavior is undefined unless the objects in the array pointed to by base are of trivial type.
- 4 Throws: Any exception thrown by compare() (20.5.12).

SEE ALSO: ISO C 7.22.5.
