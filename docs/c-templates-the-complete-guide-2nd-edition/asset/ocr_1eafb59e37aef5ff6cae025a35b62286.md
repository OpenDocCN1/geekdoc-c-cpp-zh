+   - Objects with this property can produce a reliable hash value by hashing the associated byte sequence (there is no risk that some bits not participating in the object value might differ from one case to another).
+   - Requires that the given type is trivially copyable (see Section D.3.1 on page 712) and either complete (see Section 10.3.1 on page 154) or (cv-qualified) void or an array of unknown bounds.
+   - Available since C++17.

# std:: alignment_of < T >::value

+   - Yields the alignment value of an object of type T as std::size_t (for arrays, the element type; for references, the referenced type).
+   - Same as: alignof(T)
+   - This trait was introduced in C++11 before the alignof(...) construct. It is still useful, however, because the trait can be passed around as a class type, which is useful for certain metaprograms.
+   - Requires that alignof(T) is a valid expression.
+   - Use aligned_union<> to get the common alignment of multiple types (see Section D.5 on page 733).

# std:: rank < T >::value

+   - Yields the number of dimensions of an array of type T as std::size_t.
+   - Yields 0 for all other types.
+   - Pointers do not have any associated dimensions. An unspecified bound in an array type does specify a dimension. (As usual, a function parameter declared with an array type does not have an actual array type, and std::array is not an array type either. See Section D.2.1 on page 704.) For example:

Click here to view code image

```
int a2[5][7];
rank_v<decltype(a2)>; // yields 2
rank_v<int*>; // yields 0 (no array)
extern int p1[];
rank_v<decltype(p1)>; // yields1
```

# std:: extent < T >::value
std:: extent < T, IDX >::value

+   - Yields the size of the first or IDX-th dimension of an array of type T as std::size_t.
+   - Yields 0, if T is not an array, the dimension doesn’t exist, or the size of the