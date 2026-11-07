
### Table G.6 Operations Defined for Some Sequences

| Operation | Description | Container |
| --- | --- | --- |
| `a.emplace_back(args)` | Appends an object of type T using the T constructor with the arguments packed into args. | vector, list, deque |
| `a.push_front(t)` | Inserts a copy of t before the first element. | forward_list, list, deque |
| `a.push_front(rv)` | Inserts a copy of rv before the first element. Move semantics may be used. | forward_list, list, deque |
| `a.emplace_front(args)` | Inserts in the front an object of type T using the T constructor with the arguments packed into args. | forward_list, list, deque |
| `a.pop_front()` | Erases the first element. | forward_list, list, deque |
| `a[n]` | Returns `*(a.begin() + n)`. | vector, deque, array |
| `a.at(n)` | Returns `*(a.begin() + n)`; throws `out_of_range` exception if `n >= a.size()`. | vector, deque, array |

The vector template additionally has the methods in Table G.7. Here, a is a vector container and n is an integer of X::size_type.

### Table G.7 Additional Operations for Vectors

| Operation | Description |
| --- | --- |
| `a.capacity()` | Returns the total number of elements the vector can hold without requiring reallocation. |
| `a.reserve(n)` | Alerts the object that memory for at least n elements is needed. After the method call, the capacity will be at least n elements. Reallocation occurs if n is greater than the current capacity. If n is greater than a.max_size(), the method throws a length_error exception. |

The list template additionally has the methods in Table G.8. Here, a and b are list containers, and T is the type stored in the list, such as int, t is a value of type T, i and j are input iterators, q2 and p are iterators, q and q1 are dereferenceable iterators, and n is an integer of X::size_type. The table uses the standard STL notation [i, j), meaning the range from i up to, but not including, j.

### Table G.8 Additional Operations for Lists

| Operation | Description |
| --- | --- |
| `a.splice(p,b)` | Moves the contents of list b to list a, inserting them before p. |
| `a.splice(p,b,i)` | Moves the element in list b pointed to by i to before position p in list a. |
| `a.splice(p,b,i,j)` | Moves the elements in the range [i, j) of list b to before position p in list a. |
| `a.remove(const T& t)` | Erases all elements in list a that have the value t. |
| `a.remove_if(Predicate pred)` | Given that i is an iterator into list a, erases all values for which pred(*i) is true. (Predicate is a Boolean function or function object, as discussed in Chapter 15, "Friends, Exceptions, and More.") |
| `a.unique()` | Erases all but the first element from each group of consecutive equal elements. |
| `a.unique(BinaryPredicate bin_pred)` | Erases all but the first element from each group of consecutive elements for which bin_pred(*i, *(i - 1)) is true. (BinaryPredicate is a Boolean function or function object, as discussed in Chapter 15.) |
| `a.merge(b)` | Merges the contents of list b with list a, using the < operator defined for the value type. If an element in a is equivalent to an element in b, the element from a is placed first. List b is empty after the merge. |
| `a.merge(b, Compare comp)` | Merges the contents of list b with list a, using the comp function or function object. If an element in a is equivalent to an element in b, the element from a is placed first. List b is empty after the merge. |
| `a.sort()` | Sorts list a, using the < operator. |
| `a.sort(Compare comp)` | Sorts list a, using the comp function or function object. |
| `a.reverse()` | Reverses the order of the elements in list a. |

The forward-list operations are similar. However, because a forward_list template class iterator can't go backwards, some methods have to be adjusted. Thus, the insert(), erase(), and splice() methods are replaced with the insert_after(), erase_after(), and splice_after() methods, all of which operate on the position following an iterator position rather than preceding it.

## Additional Operations for Sets and Maps

Associative containers, of which sets and maps are models, have a `Key` template parameter and a `Compare` template parameter, which indicate, respectively, the type of the key used to order the contents and the function object, termed a *comparison object*, used to compare key values. For the `set` and `multiset` containers, the stored keys are the stored values, so the key type is the same as the value type. For the `map` and `multimap` containers, the stored values of one type (template parameter `T`) are associated with a key type (template parameter `Key`), and the value type is `pair<const Key, T>`. Associative containers have additional members to describe these features, as listed in Table G.9.

### Table G.9 Types Defined for Associative Containers

| Type | Value |
| --- | --- |
| `X::key_type` | `Key`, the key type |
| `X::key_compare` | `Compare`, which has a default value of `less<key_type>` |
| `X::value_compare` | A binary predicate type that is the same as `key_compare` for `set` and `multiset`, and that supplies ordering for the `pair<const Key, T>` values in a `map` or `multimap` container |
| `X::mapped_type` | `T`, the type of the associated data (`map` and `multimap` only) |

Associative containers provide the methods listed in Table G.10. In general, the comparison object need not require that values with the same key be identical; the term *equivalent keys* means that two values, which may or may not be equal, have the same key. In the table, `X` is a container class, and `a` is an object of type `X`. If `X` uses unique keys (that is, `set` or `map`), `a_uniq` is an object of type `X`. If `X` uses multiple keys (that is, `multiset` or `multimap`), `a_eq` is an object of type `X`. As before, `i` and `j` are input iterators referring to elements of `value_type`, `[i, j)` is a valid range, `p` and `q2` are iterators to `a`, `q` and `q1` are dereferenceable iterators to `a`, `[q1, q2)` is a valid range, `t` is a value of `X::value_type` (which may be a pair), and `k` is a value of `X::key_type`. Also `il` is an `initializer_list<value_type>` object.

### Table G.10 Operations Defined for Sets, Multisets, Maps, and Multimaps

| Operation | Description |
| --- | --- |
| `X(i,j,c)` | Constructs an empty container, inserts the elements from the range `[i,j)`, and uses `c` as the comparison object. |
| `X a(i,j,c)` | Constructs an empty container (`a`), inserts the elements from the range `[i,j)`, and uses `c` as the comparison object. |
| `X(i,j)` | Constructs an empty container, inserts the elements from the range `[i,j)`, and uses `Compare()` as the comparison object. |
| `X a(i,j)` | Constructs an empty container (`a`), inserts the elements from the range `[i,j)`, and uses `Compare()` as the comparison object. |
| `X(il)` | Same as `X(il.begin(), il.end())`. |
| `a = il` | Assigns the range `il.begin(), il.end()` to `a`. |
| `a.key_comp()` | Returns the comparison object used in constructing `a`. |
| `a.value_comp()` | Returns an object of the `value_compare` type. |
| `a_uniq.insert(t)` | Inserts the value `t` into the container `a` if and only if `a` does not yet contain a value with an equivalent key. The method returns a value of type `pair<iterator,bool>`. The `bool` component is `true` if insertion occurred and `false` otherwise. The iterator component points to the element whose key is equivalent to the key of `t`. |
| `a_eq.insert(t)` | Inserts `t` and returns an iterator that points to its location. |
| `a.insert(p,t)` | Inserts `t`, using `p` as a hint to where `insert()` should begin its search. If `a` is a container with unique keys, insertion takes place if and only if `a` doesn't contain an element with an equivalent key; otherwise, insertion takes place. Whether or not insertion takes place, the method returns an iterator that points to the location with an equivalent key. |
| `a.insert(i,j)` | Inserts elements from the range `[i,j)` into `a`. |
| `a.insert(il)` | Inserts elements from the `initializer_list` `il` into `a`. |
| `a_uniq.emplace(args)` | Like `a_uniq.insert(t)`, but uses the `T` constructor whose parameter list matches the contents of the `args` parameter pack. |
| `a_eq.emplace(args)` | Like `a_eq.insert(t)`, but uses the `T` constructor whose parameter list matches the contents of the `args` parameter pack. |
| `a.emplace_hint(p,args)` | Like `a.insert(p,t)`, but uses the `T` constructor whose parameter list matches the contents of the `args` parameter pack. |
| `a.erase(k)` | Erases all elements in `a` whose keys are equivalent to `k` and returns the number of elements erased. |
