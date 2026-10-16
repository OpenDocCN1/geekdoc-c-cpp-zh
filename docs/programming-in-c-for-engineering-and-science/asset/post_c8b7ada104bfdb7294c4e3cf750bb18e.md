
```
istr >> s
```

Extracts characters from istr and stores them in s until s.max_size() characters have been extracted, the end of file occurs, or a white-space character is encountered, in which case the white-space character is not removed from istr; returns istr

```
ostr << s
```

Inserts characters of s into ostr; returns ostr

```
s = val
```

Assigns a copy of val to s; val may be a string, a character array, or a character

```
s += val
```

Appends a copy of val to s; val may be a string, a character array, or a character

```
s[pos]
```

Returns a reference to the character stored in s at position pos, provided pos < s.length()

```
s + t
t + s
```

Returns the result of concatenating s and t; t may be a string, a character array, or a character

```
s < t, t < s
s > t, t > s
s <= t, t <= s
s >= t, t >= s
s == t, t == s
s != t, t != s
```

Returns true or false as determined by the relational operator; t may be a string or a character array

```
s.append(str)
```

Appends string str at the end of s; returns s

| Member function | Description |
|---|---|
| `s.assign(str, pos, n)` | Assigns to s a copy of the n characters in str, starting at position pos; if n is too large, characters are copied only until the end of str is reached; returns s |
| `s.assign(charArray)` | Assigns to s a copy of charArray; returns s |
| `s.assign(charArray, n)` | Assigns to s a string consisting of the first n characters in charArray; returns s |
| `s.assign(n, ch)` | Assigns to s a string consisting of n copies of ch; returns s |
| `s.assign(impT1, impT2)` | Assigns to s a string consisting of the characters in the range [impT1, impT2); returns s |
| `s.at(pos)` | Returns s[pos] |
| `s.begin()` | Returns an iterator positioned at the first character in s |
| `s.c_str()` | Returns (the base address of) a char array containing the characters stored in s, terminated by a null character |
| `s.capacity()` | Returns the size (of type size_type) of the storage allocated in s |
| `s.clear()` | Removes all the characters in s; return type is void |
| `s.compare(str)` | Returns a negative value, 0, or a positive value according as s is less than, equal to, or greater than str |
| `s.compare(charArray)` | Compares s and charArray as in the preceding method |
| `s.compare(pos, n, str)` | Compares strings s and str as before, but starts at position pos in s and compares only the next n characters |
| `s.compare(pos, n, charArray)` | Compares string s and charArray as in the preceding method |
| `s.compare(pos1, n1, str, pos2, n2)` | Compares s and str as before, but starts at position pos1 in s, position pos2 in str, and compares only the next n1 characters in s and the next n2 characters in str |

```
s.compare(pos1, n1, charArray, n2)
```

Compares strings s and charArray as before, but using only the first n2 characters in charArray

```
s.copy(charArray, pos, n)
```

Replaces the string in s with n characters in charArray, starting at position pos or at position 0, if pos is omitted; if n is too large, characters are copied only until the end of charArray is reached; returns the number (of type size_type) of characters copied

```
s.data()
```

Returns a char array containing the characters stored in s.

```
s.empty()
```

Returns true if s contains no characters, false otherwise

```
s.end()
```

Returns an iterator positioned immediately after the last character in s

```
s.erase(pos, n)
```

Removes n characters from s, beginning at position pos (default value 0); if n is too large or is omitted, characters are erased only to the end of s; returns s

```
s.erase(it)
```

Removes the character at the position specified by it; returns an iterator positioned immediately after the erased character

```
s.find(str, pos)
```

Returns the first position ≥ pos such that the next str.size() characters of s match those in str; returns npos if there is no such position; 0 is the default value for pos

```
s.find(ch, pos)
```

Searches s as in the preceding method, but for ch

```
s.find(charArray, pos)
```

Searches s as in the preceding method, but for the characters in charArray

```
s.find_first_not_of(ch, pos)
```

Searches s as in the preceding method, but for ch

```
s.find_first_not_of(charArray, pos)
```

Searches s as in the preceding method, but for the characters in charArray

```
s.find_first_not_of(charArray, pos, n)
```

Searches s as in the preceding method, but using the first n characters in charArray; the value pos must be given

```
s.find_first_of(str, pos)
```

Returns the first position ≥ pos of a character in s that matches any character in str; returns npos if there is no such position; 0 is the default value for pos

```
s.find_first_of(ch, pos)
```

Searches s as in the preceding method, but for ch

```
s.find_first_of(charArray, pos)
```

Searches s as in the preceding method, but for the characters in charArray

```
s.find_first_of(charArray, pos, n)
```

Searches s as in the preceding method, but using the first n characters in charArray; the value pos must be given

```
s.find_last_not_of(str, pos)
```

Returns the highest position ≤ pos of a character in s that does not match any character in str; returns npos if there is no such position; npos is the default value for pos

```
s.find_last_not_of(ch, pos)
```

Searches s as in the preceding method, but for ch

```
s.find_last_not_of(charArray, pos)
```

Searches s as in the preceding method, but using the characters in charArray

```
s.find_last_not_of(charArray, pos, n)
```

Searches s as in the preceding method, but using the first n characters in charArray; the value pos must be given

```
s.find_last_of(str, pos)
```

Returns the highest position ≤ pos of a character in s that matches any character in str; returns npos if there is no such position; npos is the default value for pos

```
s.find_last_of(ch, pos)
```

Searches s as in the preceding method, but for ch

```
s.find_last_of(charArray, pos)
```

Searches s as in the preceding method, but using the characters in charArray

```
s.find_last_of(charArray, pos, n)
```

Searches s as in the preceding method, but using the first n characters in charArray; the value pos must be given

```
s.insert(pos, str)
```

Inserts a copy of str into s at position pos; returns s

```
s.insert(pos1, str, pos2, n)
```

Inserts a copy of n characters of str starting at position pos2 into s at position pos; if n is too large, characters are copied only until the end of str is reached; returns s

```
s.insert(pos, charArray, n)
```

Inserts a copy of the first n characters of charArray into s at position pos; inserts all of its characters if n is omitted; returns s

```
s.insert(pos, n, ch)
```

Inserts n copies of the character ch into s at position pos; returns s

```
s.insert(it, ch)
```

Inserts a copy of the character ch into s at the position specified by it and returns an iterator positioned at this copy

```
s.insert(it, n, ch)
```

Inserts n copies of the character ch into s at the position specified by it; return type is void

```
s.insert(it, inpIt1, inpIt2)
```

Inserts copies of the characters in the range [inpIt1, inpIt2) into s at the position specified by it; return type is void

```
s.length()
```

Returns the length (of type size_type) of s

```
s.max_size()
```

Returns the maximum length (of type size_type) of s

```
s.rbegin()
```

Returns a reverse iterator positioned at the last character in s

```
s.rend()
```

Returns a reverse iterator positioned immediately before the first character in s

```
s.replace(pos1, n1, str)
```

Replaces the substring of s of length n1 beginning at position pos1 with str; if n1 is too large, all characters to the end of s are replaced; returns s

```
s.replace(it1, it2, str)
```

Same as the preceding, but for the substring of s consisting of the characters in the range [it1, it2); returns s

| Signature | Description |
|---|---|
| `s.replace(pos1, n1, str, pos2, n2)` | Replaces a substring of s as in the preceding reference but using n2 characters in str, beginning at position pos2; if n2 is too large, characters to the end of str are used; returns s |
| `s.replace(pos1, n1, charArray, n2)` | Replaces a substring of s as before but with the first n2 characters in charArray; if n2 is too large, characters to the end of charArray are used; if n2 is omitted, all of charArray is used; returns s |
| `s.replace(it1, it2, charArray, n2)` | Same as the preceding, but for the substring of s consisting of the characters in the range [it1, it2); returns s |
| `s.replace(pos1, n1, n2, ch)` | Replaces a substring of s as before, but with n2 copies of ch |
| `s.replace(it1, it2, n2, ch)` | Same as the preceding but for the substring of s consisting of the characters in the range [it1, it2); returns s |
| `s.replace(it1, it2, inpIt1, inpIt2)` | Same as the preceding, but replaces with copies of the characters in the range [inpIt1, inpIt2); returns s |
| `s.reserve(n)` | Changes the storage allocation for s so that s.capacity() ≥ n, 0 if n is omitted; return type is void |
| `s.resize(n, ch)` | If n ≤ s.size(), truncates rightmost characters in s to make it of size n; otherwise, adds copies of character ch to end of s to increase its size to n, or adds a default character value (usually a blank) if ch is omitted; return type is void |
| `s.rfind(str, pos)` | Returns the highest position ≤ pos such that the next str.size() characters of s match those in str; returns npos if there is no such position; npos is the default value for pos |
| `s.rfind(ch, pos)` | Searches s as in the preceding method, but for ch |
| `s.rfind(charArray, pos)` | Searches s as in the preceding method, but for the characters in charArray |
