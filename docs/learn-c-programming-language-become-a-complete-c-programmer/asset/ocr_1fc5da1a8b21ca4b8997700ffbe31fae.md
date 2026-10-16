`errno` to `ERANGE` (§40.3). For example:

`stoi(“Hello, World!”);` // *throws* `std::invalid_argument`

`stoi(“12345678901234567890”);` // *throws* `std::out_of_range`; `errno=ERANGE`

`stof(“123456789e1000”);` // *throws* `std::out_of_range`; `errno=ERANGE`

The `sto*` functions encode their target type in their names. This makes them unsuitable for generic code where the target can be a template parameter. In such cases, consider `to<X>` (§25.2.5.1).

# 36.3.6 STL-like Operations

The `basic_string` provides the usual set of iterators:

`basic_string<C,Tr,A>` **String Iterators** (§iso.21.4.3)

All operations are noexcept

+   `p=s.begin()` p is an iterator to the first character of s  
+   `p=s.end()` p is an iterator to one beyond the end of s  
+   `p=s.cbegin()` p is a const_iterator to the first character  
+   `p=s.cend()` p is a const_iterator to one beyond the end of s  
+   `p=s.rbegin()` p is the beginning of the reverse sequence for s  
+   `p=s.rend()` p is the end of the reverse sequence for s  
+   `p=s.crbegin()` p is a const_iterator to the beginning of the reverse sequence for s  
+   `p=s.crend()` p is a const_iterator to the end of the reverse sequence for s

Because `string` has the required member types and the functions for obtaining iterators, `strings` can be used together with the standard algorithms (Chapter 32). For example:

```
void f(string& s)
{
    auto p = find_if(s.begin(),s.end(),islower);
    // ...
}
```

The most common operations on `strings` are supplied directly by `string`. Hopefully, these versions will be optimized for `strings` beyond what would be easy to do for general algorithms.

The standard algorithms (Chapter 32) are not as useful for strings as one might think. General algorithms tend to assume that the elements of a container are meaningful in isolation. This is typically not the case for a string.

A `basic_string` offers complex `assignment()`s:

`basic_string<C,Tr,A>` **Assignment** (§iso.21.4.6.3)

All operations return the string to which they are applied

+   `s.assign(x)` s=x ; x can be a `string`, a C-style string, or an `initializer_list<char_type>`  
+   `s.assign(move(s2))` Move: s2 is a `string`; noexcept  
+   `s.assign(s2,pos,n)` s gets the characters `s2[pos:pos+n)`  
+   `s.assign(p,n)` s gets the characters `[p:p+n)`; p is a C-style string  
+   `s.assign(n,c)` s gets n copies of the character c