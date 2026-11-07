**Table 19.4** The public interface for the set and map classes (Continued)

| Interface | set | map |
|---|:---:|:---:|
| **Iterators** |  |  |
| `iterator AS <...> :: begin()` | ✓ | ✓ |
| `iterator AS <...> :: end()` | ✓ | ✓ |
| `reverse_iterator AS <...> :: rbegin()` | ✓ | ✓ |
| `reverse_iterator AS <...> :: rend()` | ✓ | ✓ |
| **Accessing** |  |  |
| `T& AS <...> :: operator [] (const K& k) const` |  | ✓ |
| **Searching** |  |  |
| `size_type AS <...> :: count(const K& k) const` | ✓ | ✓ |
| `iterator AS <...> :: find(const K& k) const` | ✓ | ✓ |
| `iterator AS <...> :: lower_bound(const K& k) const` | ✓ | ✓ |
| `iterator AS <...> :: upper_bound(const K& k) const` | ✓ | ✓ |
| `pair <iterator, iterator> AS <...> :: equal_range(const K& k) const` | ✓ | ✓ |
| **Insertion** |  |  |
| `pair <iterator, bool> AS <...> :: insert(const K& k)` | ✓ |  |
| `pair <iterator, bool> AS <...> :: insert(const pair <const K, T> & p)` |  | ✓ |
| `iterator AS <...> :: insert(iterator hint, const K& element)` | ✓ |  |
| `void AS <...> :: insert(InputIterator first, InputIterator last)` | ✓ | ✓ |
| **Erasure** |  |  |
| `size_type AS <...> :: erase(const K& k)` | ✓ | ✓ |
| `void AS <...> :: erase(iterator pos)` | ✓ | ✓ |
| `void AS <...> :: erase(iterator first, iterator last)` | ✓ | ✓ |
| `void AS <...> :: clear()` | ✓ | ✓ |
| **Swapping** |  |  |
| `void AS <...> :: swap(AS <...> & v)` | ✓ | ✓ |
| **Global functions** |  |  |
| `bool operator oper(const AS <...> left, const AS <...> right)` | ✓ | ✓ |
| `void swap(AS <...> & c1, AS <...> & c2)` | ✓ | ✓ |

To discuss the classes set and map, we introduce a library struct named pair defined in the <utility> header. A pair defines a template struct with two template data members possibly of different types. The elements are called first and second, respectively, as shown below:

```
template <typename T1, typename T2>
struct pair
{
    T1 first;
    T2 second;
};
```