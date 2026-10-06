# ISO/IEC 14882:2017(E)

template <class ForwardIterator>
string_type transform(ForwardIterator first, ForwardIterator last) const;
Effects: As if

```
string_type str(collate<char<T>>)
    return use_facet(collate<char<T>>(), &str.begin(), &str.begin() + str.length());
```

template <class ForwardIterator>
string_type transform_primary(ForwardIterator first, ForwardIterator last) const;
Effects: If

typeid(use_facet(collate<char<T>>)) == typeid(collate_byname<char>) and of the sort returned by the collate_char::transform(first, last) is known and can be converted into a primary sort key then returns that key, otherwise returns an empty string.

template <class ForwardIterator>
string_type lookup_collatename(ForwardIterator first, ForwardIterator last) const;
Returns: a sequence of one or more characters that the collate element consisting of the character sequence designated by the iterator [first, last). Returns an empty string if the character sequence is not a valid collate.

template <class ForwardIterator>
char_class_type lookup(classname, bool equals = false);
ForwardIterator first, ForwardIterator last;

Returns: an unclassified value that represents the character classification by the character sequence. If the parameter equals is then the returned mask identifies the character classification without regard to the case of the characters being matched, otherwise it does honor the case of the characters being matched.³329 The value returned will be independent of the case of the characters in the character sequence. If the name is not recognized then returns char_class_type().

Remarks: For regex_traits<char<T>>, at least the narrow character names in Table 133 shall be recognized. For regex_traits<char<char_t>, at least the wide character names in Table 133 shall be recognized.

bool isctype(char c, char_class_type f) const;
Effects: Determines if the character c is a member of the character classification represented by f.

Returns: Given the following function:

```
// for exposition only
template<class D>
type_base::mask = convert<typename ctype<D>::char_class_type>(f);
returns a value in which each ctype::mask value corresponding to a value in f named in Table 133 is set, then the result is determined as if:
type_base m = convert<ctype<>>(f);
const ctype<char<>> ct = use_facet<ctype<char<>>(getloc(c));
if (ct.is(m, c))
    return true;
} else if (c == ct.wididen('_'))
    return true;
```

329) For example