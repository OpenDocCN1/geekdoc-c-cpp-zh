The map is here initialized by a list of key-value pairs. Note that the `value_type` of the `map` is not `double` but `pair<const string, double>`. In the next two lines, we use the bracket operator for finding the value with key `h` and for inserting a new value for `c`. The bracket operator returns a reference to the value of that key. If the key is not found, a new entry is inserted with a default-constructed value. The reference to this value is then returned. In case of `c`, we assign a value to this reference and set up the key-value pair. Then we ask for the non-existing Coulomb constant and accidentally create an entry with a zero value.

To avoid inconsistencies between the mutable and the constant overload of `[]`, the creators of STL omitted the constant overload altogether (a design choice we are not really happy with). To search keys in a constant map, we can use the classical method `find` or the C++11 method `at`. `find` is less elegant than `[]` but it saves us from accidentally inserting entries. It returns a `const_iterator` which refers to a key-value pair. If the key is not found, the `end` iterator is returned to which we should compare when the presence of the key is uncertain.

When we are sure that a key exists in the `map`, we can use `at`. It returns a reference to the value like `[]`. The key difference is that an `out_of_range` exception is thrown when the the key is not found—even when the `map` is mutable. Thus, it cannot be used to insert new entries but provides a compact interface for finding them.

When we iterate over the container, we get pairs of keys and associated values (as the values on their own would be meaningless).

=> c++17/multimap_test.cpp

When a key can be associated with multiple values, we need a `multimap`. The entries with the same key are stored next to each other so we can iterate over them. The iterator range is provided by the methods `lower_bound` and `upper_bound`. In the next example we iterate over all entries with key equals 3 and print their values:

Click here to view code image

```
multimap<int, double> mm=
{(3, 1.3), (2, 4.1), (3, 1.8), (4, 9.2), (3, 1.5)};
for (auto it = mm.lower_bound(3),
end = mm.upper_bound(3); it != end; ++it)
cout << "The value is " << it->second << '\n';
```