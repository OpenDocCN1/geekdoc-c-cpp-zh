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