# ISO/IEC 14882:2017(E)

7 Returns: An iterator which points to the element immediately following p prior to the element being erased. If no such element exists, end() is returned.

```
iterator erase(const_iterator first, const_iterator last);
```

8 Requires: first and last are valid iterators *this, defining a range [first, last).

9 Throws: Nothing.

10 Effects: Removes the characters in the range [first, last).

11 Returns: An iterator which points to the element prior to the other elements erased. If no such element exists, end() is returned.

```
void pop_back();
```

12 Requires: empty().

13 Throws: Nothing.

14 Effects: Equivalent to erase(size() - 1, 1).

# 24.3.2.6 basic_string::replace

```
basic_string replace(size_type pos1, size_type n1, const basic_string& str);
```

1 Effects: Equivalent to: replace(pos1, n1, str.data(), str.size());

```
basic_string replace(size_type pos1, size_type n1, const basic_string& str,
size_type pos2, size_type n2 = npos);
```

2 Throws: out_of_range if pos > size() or pos2 > str.size().

3 Effects: Determines the effective length len of the string to be inserted as the smaller of n2 and str.size() - pos2 and calls replace(pos1, n1, str.data() + pos2).

4 Throws: nothing.

```
basic_string replace(size_type pos1, size_type n1, const basic_view<charT, traits> sv);
```

5 Effects: Equivalent to replace(pos1, n1, sv.data(), sv.size());

```
template <class T>
basic_string replace(size_type pos1, size_type n1, const T& t,
size_type pos2, size_type n2 = npos);
```

6 Throws: out_of_range if pos > size() or pos2 > sv.size().

7 Effects: Creates a variable, as sv, by basic_view<charT, traits> traits = t. Determines the effective length of the string to be inserted as the smaller of n2 and sv.size() - pos2 and calls replace(pos1, n1, sv.data() + pos2).

8 Remarks: This function will not participate in overload resolution unless is_convertible_const<T&, basic_view<charT, traits>> is true and is_convertible_const<charT*, T> is false.

9 Throws: nothing.

```
basic_string replace(size_type pos1, size_type n1, const char* s, size_type n2);
```

10 Requires: p points to an area of at least n2 characters of charT.

11 Throws: out_of_range if pos > size() or length_error if the length of the resulting string exceed max_size() (see below).

12 Effects: Determines the effective length len of the string to be removed as the smaller of n1