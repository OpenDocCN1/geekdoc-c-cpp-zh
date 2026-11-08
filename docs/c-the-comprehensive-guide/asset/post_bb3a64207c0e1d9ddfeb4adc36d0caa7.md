
### Accessing

You have forward iterators available, as you can see in [Table 24.2](#).

- **Access via iterators**  
  With `begin()` and `end()` as well as `cbegin()` and `cend()`, you get iterators to the beginning and end of the container.
- **Access via search**  
  `find` returns any matching element to you, or you get `end()` back if there is none. For the `multi...` variants, the `count` and `equal_range` methods make sense: With `count`, you can count the number of matching elements, and with `contains`, you can check for existence. The `equal_range` method returns the range of all matching elements with a pair of iterators.

Here is an example of accessing an `unordered_multiset`:

```cpp
// https://godbolt.org/z/a8cGxr9s9
#include <unordered_set> // unordered_multiset
#include <iostream>
#include <string>
using std::unordered_multiset; using std::cout; using std::string;
int main() {
    const string s = "She sells sea shells by the seashore.";
    unordered_multiset<int> cs(s.begin(), s.end()); // string as container
    cout << cs.count('s') << " times s\n"; // Output: 7 times s
}
```

**Listing 24.87** For the “multi” variants, “count” makes perfect sense.

If creating a key is expensive and you need to do it often for searching, consider the ordered multiset. This allows you to search without creating a complete key.

### Deleting

The relative order of nondeleted elements to each other remains valid when deleting, as do iterators referencing these elements:

- **Deleting all elements**  
  `clear()` deletes all elements.
- **Deleting or transferring a single element**  
  `erase` with a value deletes *all* occurrences of that element. The return value is the number of elements deleted. If you specify an iterator, the element at that position is deleted. The return value is then the position of the next element. With `extract`, you delete an element that you would normally insert somewhere else.
- **Deleting multiple elements**  
  With a pair of iterators, you can delete multiple elements. This actually only makes sense for unordered containers if this range includes all elements, which is equivalent to `clear()`, or if the range includes all or some elements of an `equal_range`. Both are possible, but probably rather rare in practice. Deletion also works with ranges that include several different elements, but which elements lie in between is hard to predict for unordered containers.

### Speciality: By the Bucketful

You can gain detailed insights into the inner workings of the `unordered_multiset` using `bucket_count()`, `bucket_size`, and `bucket` as well as the `int` variants of `begin(int)` and `end(int)`.

### Speciality: Reserve Space

To repel unwarranted interruptions from rude reallocations of the hash table when inserting, you can manipulate the hash mechanism using the `load_factor`, `max_load_factor`, `rehash`, and `reserve` methods.

## 24.8.7 “unordered_multimap”

The `unordered_multimap` can do everything that `multimap` can do (Section 24.7.6), but as an unordered associative container, it also has an interface that is closely related to the `unordered_multiset` (Section 24.8.6).

Keys are mapped to target values, which usually takes O(1) time, but in exceptional cases can also take O(n). Instead of using less than `<`, the keys are compared using `==` and a hash function.

A key can be inserted multiple times, each time referring to different target values.

### Element Properties

As with all map-like containers, the elements of the `unordered_multimap` are of type `pair<const Key, Target>`. This means that if you have a reference to an element or a Target, you can assign a new value to Target. The Key is const and must not be changed under any circumstances; otherwise, the container will get confused.

For the key, equality `==` must be checkable and a hash must be computable. This can be done either via the free function `operator==` and the functor `std::hash<Key>`, or you can specify your own functors as template parameters. Recall that instead of `operator==`, you can simply define `operator<=>` with `= default` if the compiler's implementation supports it.

6 Under no circumstances should you change a key in such a way that the change affects `==` or the hash function.

### Initialize

The template parameters for defining an `unordered_multimap` are at least Key and Target. The compiler cannot spare you the template parameters when you use nested initializer lists for creation; it can only do so if you use `pair`.

Optionally, you can also specify `Hash`, `KeyEqual`, and `Allocator`.

The usual suspects are available as constructor overloads:

- The default constructor for an empty container
- A range from another container or stream using an iterator pair
- An initializer list with the desired values of the container
- From C++23, `from_range` and a range
- The copy and move constructors for taking over the contents of another `unordered_multimap`

The first three overloads each accept the initial size of the hash table as an optional parameter.

### Assignment

You can also assign the content of another already initialized `unordered_multimap` afterward. This copies or moves the contents. `swap` is also available to you.

### Insert

You insert similarly as with `multimap`. This also means that `[]` or `at` is not available to you:

- **Inserting a single element with automatic positioning**  
  The insert method takes a pair; emplace takes the two elements of the pair. Both always insert a new element as duplicate keys are also stored.
- **Inserting a single element with a position hint**  
  `insert` also accepts an additional iterator as a parameter; `emplace_hint` does as well. The iterator should then point to an element whose key == the new key, as the container can possibly save on hashing and searching work. If the hint does not fit, the advantage is lost, but the insertion is still correct.
- **Inserting multiple elements**  
  With a range as a parameter—that is, two iterators—or an initializer list, you can also use `insert` to insert multiple elements at once. Starting from C++23, there is also `insert_range`. With `merge`, you can retrieve all elements from another suitable container even if they are contained multiple times here.

Iterators lose their validity with each insert operation, unless you have previously ensured enough space in the hash table using `reserve`.

### Accessing

With forward iterators, not much is available to you. When you dereference them, `first` contains the key and `second` contains the target value of the element:

- **Access via iterators**  
  `begin()` and `end()` as well as `cbegin()` and `cend()` provide you with forward iterators to the beginning and end of the container.
- **Access via search**  
  `find` takes a key as a parameter and returns an iterator to one of the matching elements. `count` counts the number of matching keys, and `contains` checks if a key is present. `equal_range` returns a range containing all keys that match the searched key. For all these methods, you need a fully constructed key. Unlike `multimap`, there is no shortcut with special search functions.

### Deleting

You can delete elements in the following ways:

- **Deleting all elements**  
  With `clear()`, you remove all elements.
- **Deleting or transferring a single element**  
  With a key as a parameter, `erase` deletes all occurrences of that key; with an iterator as a parameter, it deletes only the corresponding element. You get the number of deleted elements or the element following the deleted one. `extract` is used to transfer an element to another container using `insert`.
- **Deleting multiple elements**  
  You can delete multiple elements with two iterators. This is probably of limited use with unordered associative containers, because in such a container there can be arbitrary elements between two iterators. You wouldn't know which elements you actually delete. Therefore, only when you have exactly none, one or all, elements between the two iterators, will you know which elements you're left with after the delete operation.

Iterators remain valid if their elements have not been deleted. And you can rely on the remaining elements not being rearranged. This enables use in loops.

### Speciality: By the Bucketful

You can gain insights into the hash table with `bucket_count`, `bucket_size`, and `bucket`. With `begin(int)` and `end(int)`, you get iterators to the elements of a specific bucket.

### Speciality: Reserve Space

With `reserve` or `rehash`, you can influence how large the hash table should become so that the table is not immediately rearranged during upcoming insert operations and
