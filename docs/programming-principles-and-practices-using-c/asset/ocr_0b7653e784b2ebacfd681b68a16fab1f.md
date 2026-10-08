+   • Provides `insert()`, `erase()`, `front()` and `back()`, `push_back()` and `pop_back()`, `size()`, etc.; `vector` and `map` also provide subscripting (e.g., operator []).

+   • Provides comparison operators (`==`, `!=`, `<`, `<=`, `>`, and `>=`) that compare the elements. Containers use lexicographical ordering for `<`, `<=`, `>`, and `>=`; that is, they compare the elements in order starting with the first.

The aim of this list is to give you an overview. For more detail see Appendix B. For a more precise specification and complete list, see *The C++ Programming Language* or the standard.

Some data types provide much of what is required from a standard container, but not all. We sometimes refer to those as “almost containers.” The most interesting of those are:

| “Almost containers” | | |
|---|---|---|
| `T[n]` built-in array | | no `size()` or other member functions; prefer a container, such as `vector`, `string`, or `array`, over a built-in array when you have a choice |
| `string` | | holds only characters but provides operations useful for text manipulation, such as concatenation (`+` and `+=`); prefer the standard string to other strings |
| `valarray` | | a numerical vector with vector operations, but with many restrictions to encourage high-performance implementations; use only if you do a lot of vector arithmetic |

In addition, many people and many organizations have produced containers that meet the standard container requirements, or almost do so.
If in doubt, use `vector`. Unless you have a solid reason not to, use `vector`.

# 20.10.1 Iterator categories

We have talked about iterators as if all iterators are interchangeable. They are interchangeable if you do only the simplest operations, such as traversing a sequence once reading each value once. If you want to do more, such as iterating backward or subscripting, you need one of the more advanced iterators.